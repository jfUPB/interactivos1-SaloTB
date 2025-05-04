## Coneccion ocn mirco:bit 

### Ejemplo elejido
https://openprocessing.org/sketch/2541284 
https://editor.p5js.org/SaloTB/full/TGu7hHqeh 

### Modificacion
	let port, reader;
	let microBitX = 0, microBitY = 0;
	let microBitA = false, microBitB = false;
	let S, H;
	let pal, BG;
	let speedFactor = 1;
	let lastButtonB = false;
	let scaleFactor = 1;
	
	let connectBtn;
	let isMicrobitConnected = false;
	
	function setup() {
	  createCanvas(S = min(windowWidth, windowHeight), S);
	  frameRate(30);
	  randomSeed(~~random(hour() + minute() + second()));
	  noiseSeed(random(1234567));
	  S /= 7;
	  H = S / 2 * sqrt(3);
	  pal = random(palettes);
	  BG = random(pal);
	  noFill();
	  strokeCap(PROJECT);
	
	  connectBtn = createButton("Conectar micro:bit");
	  connectBtn.position(10, 10);
	  connectBtn.mousePressed(connectMicrobit);
	}
	
	async function connectMicrobit() {
	  try {
	    port = await navigator.serial.requestPort();
	    await port.open({ baudRate: 115200 });
	    reader = port.readable
	      .pipeThrough(new TextDecoderStream())
	      .getReader();
	
	    isMicrobitConnected = true;
	    connectBtn.html("Desconectar");
	    readLoop();
	
	    console.log('Micro:bit conectado');
	  } catch (err) {
	    console.error('Error al conectar:', err);
	  }
	}
	
	async function readLoop() {
	  try {
	    while (port.readable) {
	      const { value, done } = await reader.read();
	      if (done) break;
	      if (value) parseMicrobitData(value);
	    }
	  } catch (error) {
	    console.error('Error leyendo datos:', error);
	  } finally {
	    reader.releaseLock();
	    port.close();
	    isMicrobitConnected = false;
	    connectBtn.html("Conectar micro:bit");
	  }
	}
	
	function parseMicrobitData(raw) {
	  let lines = raw.trim().split("\n");
	  lines.forEach(line => {
	    let values = line.trim().split(",");
	    if (values.length === 4) {
	      microBitX = parseInt(values[0]);
	      microBitY = parseInt(values[1]);
	      microBitA = values[2] === "1";
	      microBitB = values[3] === "1";
	
	      // Movimiento: escala y velocidad
	      scaleFactor = map(abs(microBitY), 0, 1024, 0.5, 2);
	      speedFactor = map(abs(microBitX), 0, 1024, 0.2, 3);
	
	      if (microBitA) {
	        pal = random(palettes);
	        BG = random(pal);
	      }
	
	      if (microBitB && !lastButtonB) {
	        speedFactor += 0.5;
	        if (speedFactor > 3) speedFactor = 0.5; // ciclo
	      }
	
	      lastButtonB = microBitB;
	    }
	  });
	}
	
	function draw() {
	  let clr = color(BG);
	  let darkenBG = color(red(clr) / 6, green(clr) / 6, blue(clr) / 6);
	  background(darkenBG);
	  fill(BG);
	  noStroke();
	  rect(0, 0, width, height);
	
	  let offsetX = map(microBitX, -1024, 1024, -width / 4, width / 4);
	  let offsetY = map(microBitY, -1024, 1024, -height / 4, height / 4);
	
	  const shapesImg = getKaleidoscopeImg(35, offsetX, offsetY);
	  const dx = 3 * S;
	  const dy = H;
	
	  for (let y = 0, j = 0; y < height; y += dy, j++) {
	    for (let x = 0; x < width; x += dx) {
	      drawKaleidoscope(shapesImg, x + (j % 2 === 0 ? 0 : dx / 2), y);
	    }
	  }
	
	  strokeWeight(H);
	  stroke(0, 56);
	
	  let l = { x: 2 * S * scaleFactor, y: -4 * H * scaleFactor };
	  for (let i = -6; i < 6; i++) {
	    let p = {
	      x: width / 2 + i * S + offsetX / 2,
	      y: height / 2 + offsetY / 2
	    };
	    for (let j = 0; j < abs(i); j++) {
	      line(p.x - l.x, p.y - l.y, p.x + l.x, p.y + l.y);
	      line(p.x - l.x, p.y + l.y, p.x + l.x, p.y - l.y);
	    }
	  }
	}
	
	function getKaleidoscopeImg(numLines) {
	  push();
	  clip(() => {
	    triangle(width / 2 - S / 2, height / 2, width / 2, height / 2 - H, width / 2 + S / 2, height / 2);
	  });
	
	  strokeWeight(S / 7 * scaleFactor);
	  for (let i = 0; i < numLines; i++) {
	    const t = frameCount / (60 / speedFactor);
	    const n1 = noise(1234, i, t) * 2 - 0.5;
	    const n2 = noise(2234, i, t) * 2 - 0.5;
	    const n3 = noise(3234, i, t) * 2 - 0.5;
	    const n4 = noise(4234, i, t) * 2 - 0.5;
	    stroke(pal[i % pal.length]);
	    strokeWeight((10 - i) * scaleFactor);
	    line(width / 2 + (n1 - 0.5) * S, height / 2 - n2 * H, width / 2 + (n3 - 0.5) * S, height / 2 - n4 * H);
	
	    const n5 = noise(5234, i, t) * 2 - 0.5;
	    const n6 = noise(6234, i, t) * 2 - 0.5;
	    stroke(pal[pal.length - i % pal.length - 1]);
	    strokeWeight((6 - i / 2) * 1.5 * scaleFactor);
	    point(width / 2 + (n5 - 0.5) * S, height / 2 - n6 * H);
	  }
	
	  strokeWeight(1);
	  stroke(32, 128);
	  noFill();
	  triangle(width / 2 - S / 2, height / 2, width / 2, height / 2 - H, width / 2 + S / 2, height / 2);
	  pop();
	
	  return get(width / 2 - S / 2, height / 2 - H, S, S);
	}
	
	function drawKaleidoscope(shapesImg, px, py) {
	  for (let i = 0; i < 6; i++) {
	    push();
	    translate(px, py);
	    rotate(i * TAU / 6);
	    clip(() => {
	      triangle(0, 0, S / 2, H, -S / 2, H);
	    });
	    if (i % 2 === 1) scale(-1, 1);
	    image(shapesImg, -S / 2, 0);
	    pop();
	  }
	}

	const palettes = [
		["#8386f5", "#3d43b4", "#04134b", "#083e12", "#1afe49"],
		["#f887ff", "#de004e", "#860029", "#321450", "#29132e"],
		["#e96d5e", "#ff9760", "#ffe69d", "#6a7e6a", "#393f5f"],
		["#ff124f", "#ff00a0", "#fe75fe", "#7a04eb", "#120458"],
		["#ff6e27", "#fbf665", "#73fffe", "#6287f8", "#383e65"],
		["#7700a6", "#fe00fe", "#defe47", "#00b3fe", "#0016ee"],
		["#63345e", "#ac61b9", "#b7c1de", "#0b468c", "#092047"],
		["#af43be", "#fd8090", "#c4ffff", "#08deea", "#1261d1"],
		["#a0ffe3", "#65dc98", "#8d8980", "#575267", "#222035"],
		["#ff2a6d", "#d1f7ff", "#f5d9e8", "#005678", "#01012b"],
		["#490109", "#d40011", "#fd7495", "#5e4ef8", "#14029a"],
		["#8f704b", "#daae6d", "#89e3f6", "#4d9e9b", "#44786a"],
		["#fff69f", "#fdd870", "#d0902f", "#a15501", "#351409"],
		["#b0acb0", "#e2dddf", "#85ebd9", "#3d898d", "#2f404d"],
		["#ff184c", "#ff577d", "#ffccdc", "#0a9cf5", "#003062"]
	]
