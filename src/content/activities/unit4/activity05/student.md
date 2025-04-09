## Coneccion ocn mirco:bit 

### Ejemplo elejido
https://openprocessing.org/sketch/2541284 

### Modificacion
     let pal, palette, BG;
    let S, H;
    let port;
    let connectBtn;
    
    let microBitX = 0;
    let microBitY = 0;
    let microBitAState = false;
    let microBitBState = false;
    let prevA = false;
    let prevB = false;
    
    let appState = "WAIT_MICROBIT";
    let palettes = [
      ["#264653", "#2a9d8f", "#e9c46a", "#f4a261", "#e76f51"],
      ["#ffbe0b", "#fb5607", "#ff006e", "#8338ec", "#3a86ff"],
      ["#ffadad", "#ffd6a5", "#fdffb6", "#caffbf", "#9bf6ff"]
    ];
    
    function setup() {
      createCanvas(windowWidth, windowHeight);
      frameRate(30);
      S = min(windowWidth, windowHeight) / 7;
      H = S / 2 * sqrt(3);
    
      palette = random(palettes);
      BG = random(palette);
      noFill();
      strokeCap(PROJECT);
    
      port = createSerial();
      connectBtn = createButton("Conectar micro:bit");
      connectBtn.position(10, 10);
      connectBtn.mousePressed(() => {
        if (!port.opened()) {
          port.open("MicroPython", 115200);
        } else {
          port.close();
        }
      });
    }
    
    function draw() {
      if (port.opened()) {
        if (appState === "WAIT_MICROBIT") {
          console.log("Micro:bit conectado");
          appState = "RUNNING";
        }
    
        if (port.availableBytes() > 0) {
          let data = port.readUntil("\n");
          if (data) {
            let values = data.trim().split(",");
            if (values.length === 4) {
              microBitX = int(values[0]) + width / 2;
              microBitY = int(values[1]) + height / 2;
              microBitAState = values[2].toLowerCase() === "true";
              microBitBState = values[3].toLowerCase() === "true";
              handleButtons();
            }
          }
        }
      } else {
        appState = "WAIT_MICROBIT";
        return;
      }
    
      if (appState === "RUNNING" && microBitAState) {
        let clr = palette[int(random(palette.length))];
        stroke(clr);
        drawKaleidoscope(microBitX, microBitY);
      }
    }
    
    function handleButtons() {
      // A PRESSED
      if (microBitAState && !prevA) {
        console.log("A presionado: dibujar activado");
      }
    
      // B RELEASED
      if (!microBitBState && prevB) {
        console.log("B soltado: guardar imagen + nueva paleta");
        saveCanvas("kaleido_" + Date.now(), "png");
        palette = random(palettes);
        BG = random(palette);
      }
    
      prevA = microBitAState;
      prevB = microBitBState;
    }
    
    function drawKaleidoscope(px, py) {
      let shapesImg = getKaleidoscopeImg(30);
      const dx = 3 * S;
      const dy = H;
      let darkenBG = color(red(BG)/6, green(BG)/6, blue(BG)/6);
      background(darkenBG);
    
      for (let y = 0, j = 0; y < height; y += dy, j++) {
        for (let x = 0; x < width; x += dx) {
          let offset = (j % 2 === 0 ? 0 : dx / 2);
          drawTile(shapesImg, x + offset, y);
        }
      }
    }
    
    function getKaleidoscopeImg(numLines) {
      let pg = createGraphics(S, H);
      pg.strokeWeight(S / 8);
      for (let i = 0; i < numLines; i++) {
        pg.stroke(palette[i % palette.length]);
        let x1 = random(S);
        let y1 = random(H);
        let x2 = random(S);
        let y2 = random(H);
        pg.line(x1, y1, x2, y2);
      }
      return pg;
    }
    
    function drawTile(img, px, py) {
      for (let i = 0; i < 6; i++) {
        push();
        translate(px, py);
        rotate(i * PI / 3);
        if (i % 2 === 1) scale(-1, 1);
        image(img, -S / 2, 0);
        pop();
      }
    }
