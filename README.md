## xperiment : 000 :
https://twitter.com/nicolasbaez/status/1372649982856212481?s=20

![twitter](https://github.com/nicolasbaez/xperiment000/blob/main/xperiment000.gif)
```processing
int q=128;
float zMin;
float zMax;
float vMax=7;
float w[]=new float[q];
float xx[]=new float[q];
float yy[]=new float[q];
float zz[]=new float[q];
float dx[]=new float[q];
float dy[]=new float[q];
float dz[]=new float[q];
float rr;
float gg;
float bb;
float dr;
float dg;
float db;
void setup() {
  size(512, 512, P3D);
  smooth();
  zMin=width;                               
  zMax=width;
  rr=random(360);
  gg=random(360);
  bb=random(360);
  dr=random(vMax);
  dg=random(vMax);
  db=random(vMax);
  for (int i=0; i<q; i++) {
    xx[i]=width/2;
    yy[i]=height/2;
    zz[i]=random(-width);
    w[i]=int(random(width*0.1, width*0.15));
    dx[i]=random(-vMax, vMax);
    dy[i]=random(-vMax, vMax);
    dz[i]=random(vMax);
  }
}
void draw() {
  clear();
  noStroke();
  directionalLight(map(sin(radians(rr)), -1, 1, 0, 255), map(sin(radians(gg)), -1, 1, 0, 255), map(sin(radians(bb)), -1, 1, 0, 255), sin(radians(rr)), sin(radians(gg)), sin(radians(bb)));
  // ambientLight(255-rr, 255-gg, 255-bb);
  for (int i=0; i<q; i++) {
    pushMatrix();
    translate(xx[i], yy[i], zz[i]);
    sphere(w[i]);
    popMatrix();
    xx[i]+=dx[i];
    yy[i]+=dy[i];
    zz[i]+=dz[i];
    if (zz[i]<=-zMin||zz[i]>=zMax) {
      xx[i]=width/2;
      yy[i]=height/2;
      zz[i]=-width;
      w[i]=int(random(width*0.1, width*0.15));
      dx[i]=random(-vMax, vMax);
      dy[i]=random(-vMax, vMax);
      dz[i]=random(vMax);
    }
  }
  rr+=dr;
  if (rr>=360) {
    rr=0;
    dr=random(vMax);
  }
  gg+=dg;
  if (gg>=360) {
    gg=0;
    dg=random(vMax);
  }
  bb+=db;
  if (bb>=360) {
    bb=0;
    db=random(vMax);
  }
  if (frameCount<=1000) {
    saveFrame("gif/xp000-######.png");
  }
}

```
