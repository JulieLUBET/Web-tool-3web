# T1 - Creative coding Web tool - 3web

## 1. Idées :

- Image Glitcher :
importer une image et la "casser" en jouant sur les pixels, couleurs, distortions

- Mood Blender :
importer une ou plusieurs images puis générer automatiquement une palette de couleur d'ambiance (dominantre + secondaire) + "mood" (chaeureux, froid, vintage)
    - un outil qui analyse plusieur images pour en extraire une ambiance global. (+ proposition d'image ou suggestion)
    - Mood Composer : l'ambiance devient un son. Importation des images -> l'outil capte l'ambiance -> génération du son/de la musique.
    - Mood Narrator - l'outil raconte l'ambiance : l'outil génére un mini texte poétique ou descriptif à partir des couleurs dominantes et de la luminausité
    - donner les données moyenne (lumière, saturation, texture, température des couleurs)
    - Fusion émotionnelle visuelle : chanque image devient un nuage de particules colorées -> l'outil fusionne ces nuages pour créer une composition abstraite.

## 2. Description de l'outil
Cet outil permet d’analyser et transformer une ou plusieurs images afin d’extraire une ambiance visuelle, sonore et narrative.

Grâce à plusieurs modules :

- Analyse de couleurs : extraction des tons dominants, saturation moyenne, luminosité, température.
- Synthèse visuelle : génération d'une palette de couleurs + nuage de particules.
- Synthèse narrative : création d’une courte description ou d’un titre poétique inspiré des couleurs.
- Synthèse musicale : production d’une ambiance sonore dérivée des données colorimétriques.

Chaque image est stockée et analysée individuellement, puis les données sont combinées si plusieurs images sont importées pour produire une ambiance moyenne.

## 3. Les snippets
Découpage des bouts de code pour le projet (fonctionnalités) :
- donner les images avec recherches sur bureau / ou liens
```
let img;

function preload() {
  img = loadImage('assets/image.jpg');
}

function setup() {
  createCanvas(600, 400);
}

function draw() {
  background(20);
  image(img, 0, 0, width, height);
}
```

- générer un nuancier
```
function getAverageColor(img) {
  img.loadPixels();
  let r = 0, g = 0, b = 0;
  const step = 4;

  for (let i = 0; i < img.pixels.length; i += step*50) {
    r += img.pixels[i];
    g += img.pixels[i+1];
    b += img.pixels[i+2];
  }

  const count = img.pixels.length / (step*50);
  return [r/count, g/count, b/count];
}
```

- générer un titre/texte poétique
```
function generateTitle(lum) {
  if (lum < 80) return "Crépuscule Éteint";
  if (lum < 150) return "Brume Pastel";
  return "Aube Montante";
}
```

- générer un son
```
let osc;

function setup() {
  createCanvas(200, 200);
  osc = new p5.Oscillator('sine');
}

function mousePressed() {
  osc.freq(random(200, 600));
  osc.start();
}

function mouseReleased() {
  osc.stop();
}
```

- Particules (Fusion émotionnelle visuelle)
```
let particles = [];

function setup() {
  createCanvas(600, 400);
  for (let i=0; i<200; i++) {
    particles.push({
      x: random(width),
      y: random(height),
      col: color(random(255), random(255), random(255))
    });
  }
}

function draw() {
  background(10);
  particles.forEach(p => {
    fill(p.col);
    noStroke();
    ellipse(p.x, p.y, 4);
    p.x += random(-1, 1);
    p.y += random(-1, 1);
  });
}
```

### Support :
- [Cour](https://nicolas-tilly.notion.site/T1-creative-coding-3Web-27ee9045f87180e08cede8044f454e1c)
- [p5.js](https://p5js.org/reference/#/p5/loadImage)
- [thecodingtrain](https://thecodingtrain.com/tracks)

