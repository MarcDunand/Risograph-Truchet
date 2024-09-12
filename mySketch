let pinkLayer;
let tealLayer;
let paperLayer; // you won't need this unless you want to do knockouts

function setup() {
	width = 2448;
	height = 3168;
  createCanvas(width, height); // 8.5x11 @72dpi
  pixelDensity(1);
  background("white");
	curveTightness(-1);
	noFill();
	strokeWeight(5);
	stroke(50);
  // Setup Riso. 
  pinkLayer = new Riso("fluorescentpink");
  tealLayer = new Riso("teal");
  paperLayer = new Riso("white");

	pinkLayer.stroke(255);
	pinkLayer.strokeWeight(6);
	pinkLayer.noFill();
	pinkLayer.curveTightness(-1);
	
	tealLayer.stroke(255);
	tealLayer.strokeWeight(10);
	tealLayer.noFill();
	tealLayer.curveTightness(-1);
	
	clearRiso();
	tealLayer.push();
	pinkLayer.push();
	background(255);
	tealLayer.translate(144, 144);
	pinkLayer.translate(144, 144);
	for(let y = 0; y < 24; y++) {
		tealLayer.push();
		pinkLayer.push();
		for(let x = 0; x < 18; x++) {
			makeTile(120, 120, [x, y]);
			tealLayer.translate(120, 0);
			pinkLayer.translate(120, 0);
		}
		pinkLayer.pop();
		tealLayer.pop();
		tealLayer.translate(0, 120);
		pinkLayer.translate(0, 120);
	}
	pinkLayer.pop();
	tealLayer.pop();
	drawRiso();
	
}


function makeTile(tWidth, tHeight, pr) {
	P = [];
	for(let x = 1; x < 4; x++) {
		append(P, Object.freeze({ x:x*(tWidth/4), y:0 }));
		append(P, Object.freeze({ x:x*(tWidth/4), y:tHeight }));
	}
	
	for(let y = 1; y < 4; y++) {
		append(P, Object.freeze({ x:0, y:y*(tHeight/4) }));
		append(P, Object.freeze({ x:tWidth, y:y*(tHeight/4) }));
	}
	append(P, Object.freeze({ x:0, y:0 }));
	append(P, Object.freeze({ x:0, y:tHeight }));
	append(P, Object.freeze({ x:tWidth, y:0 }));
	append(P, Object.freeze({ x:tWidth, y:tHeight }));
	
	
	var p1;
	var p2;
	var p3;
	var p4;
	
	var p2Vert;
	var p3Vert;
	
	for(let i = 0; i < 16; i+=1) {
		for(let j = 0; j < 16; j+=1) {
			pval= noise(pr[0]/4.5 + i/60, pr[1]/6 + j/60);
			if(random(0, 25) < pval && pval > 0.3) {
				p2 = P[i];
				p3 = P[j];
				
				if(!(p2.x == p3.x && p2.y == p3.y)) {

					if(p2.x == 0) {
						p1 = Object.freeze({ x:(-1*p3.x), y:p3.y });
						p2Vert = true;
					}
					if(p2.x == tWidth) {
						p1 = Object.freeze({ x:(tWidth*2 - p3.x), y:p3.y });
						p2Vert = true;
					}
					if(p2.y == 0) {
						p1 = Object.freeze({ x:p3.x, y:(-1*p3.y) });
						p2Vert = false;
					}
					if(p2.y == tHeight) {
						p1 = Object.freeze({ x:p3.x, y:(tHeight*2 - p3.y) });
						p2Vert = false;
					}

					if(p3.x == 0) {
						p4 = Object.freeze({ x:(-1*p2.x), y:p2.y });
						p3Vert = true;
					}
					if(p3.x == tWidth) {
						p4 = Object.freeze({ x:(tWidth*2 - p2.x), y:p2.y });
						p3Vert = true;
					}
					if(p3.y == 0) {
						p4 = Object.freeze({ x:p2.x, y:(-1*p2.y) });
						p3Vert = false;
					}
					if(p3.y == tHeight) {
						p4 = Object.freeze({ x:p2.x, y:(tHeight*2 - p2.y) });
						p3Vert = false;
					}

					tealLayer.curve(p1.x, p1.y, p2.x, p2.y, p3.x, p3.y, p4.x, p4.y);
					let dif;
					if (random() < 0.25) {
						dif = -1*(tWidth/8);
						pinkLayer.curve(p1.x + dif, p1.y + dif, p2.x + dif, p2.y + dif, p3.x + dif, p3.y + dif, p4.x + dif, p4.y + dif);
					}
					else if (random() < 0.5) {
						dif = tWidth/8;
						pinkLayer.curve(p1.x + dif, p1.y + dif, p2.x + dif, p2.y + dif, p3.x + dif, p3.y + dif, p4.x + dif, p4.y + dif);
					}
					else if (random() < 0.75) {
						dif = -1*(tWidth/8);
						pinkLayer.curve(p1.x + dif, p1.y - dif, p2.x + dif, p2.y - dif, p3.x + dif, p3.y - dif, p4.x + dif, p4.y - dif);
					}
					else {
						dif = tWidth/8;
						pinkLayer.curve(p1.x + dif, p1.y - dif, p2.x + dif, p2.y - dif, p3.x + dif, p3.y - dif, p4.x + dif, p4.y - dif);
					}
				}
				else {
					pinkLayer.push();
					pinkLayer.fill(50);
					pinkLayer.noStroke();
					pinkLayer.circle(0, 0, int(random(0, 9))*(tWidth/8));
					pinkLayer.pop();
				}
			}
		}
	}
	
	
	
}

function keyPressed() {
	if (key == "s") {
		exportRiso();
	}
}
