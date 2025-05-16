# Crear la bomba en p5.js
    let state;
    const STATE_CONFIG = 0;
    const STATE_ARMED = 1;
    const STATE_EXPLODED = 2;
    
    let countdownTime = 20;
    let minTime = 10;
    let maxTime = 60;
    let startTime;
    let inputSequence = [];
    const desarmarSecuencia = ["A", "B", "A", "S"];
    let displayText = "💣 20s";
    
    function setup() {
        createCanvas(500, 500);
        background(220);
        textSize(32);
        textAlign(CENTER, CENTER);
        
        state = STATE_CONFIG;
       
        displayText = "💣 20s"
        // Botones
        let btnA = createButton("A");
        btnA.position(180, 300);
        btnA.mousePressed(() => handleInput("A"));
    
        let btnB = createButton("B");
        btnB.position(220, 300);
        btnB.mousePressed(() => handleInput("B"));
    
        let btnS = createButton("S");
        btnS.position(260, 300);
        btnS.mousePressed(() => handleInput("S"));
    
        let btnT = createButton("T");
        btnT.position(300, 300);
        btnT.mousePressed(() => handleInput("T"));
    }
    
    function draw() {
        background(220);
        text(displayText, width / 2, height / 2);
        
        if (state === STATE_ARMED) {
            let elapsedTime = (millis() - startTime) / 1000;
            let remainingTime = countdownTime - elapsedTime;
            if (remainingTime > 0) {
                displayText = "⏳" + Math.ceil(remainingTime) + "s";
            } else {
                state = STATE_EXPLODED;
                displayText = "💀 BOOM!";
            }
        }
    }
    
    function handleInput(input) {
        if (state === STATE_CONFIG) {
            if (input === "A" && countdownTime < maxTime) countdownTime++;
            if (input === "B" && countdownTime > minTime) countdownTime--;
            if (input === "S") {
                state = STATE_ARMED;
                startTime = millis();
                inputSequence = [];
            }
            displayText = "💣 " + countdownTime + "s";
        }
    
        if (state === STATE_ARMED) {
            if (input === desarmarSecuencia[inputSequence.length]) {
                inputSequence.push(input);
    
                if (inputSequence.length === desarmarSecuencia.length) {
                    state = STATE_CONFIG;
                    countdownTime = 20;
                    inputSequence = [];
                    displayText = "😃 Disarmed!"
                }
            } else {
                inputSequence = []; // Reinicia la secuencia si se ingresa algo incorrecto
            }
        }
    
        if (state === STATE_EXPLODED && input === "T") {
            state = STATE_CONFIG;
            countdownTime = 20;
            displayText = "💣 20s";
        }
    }
