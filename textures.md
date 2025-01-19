# Textúry
Objekty používané na pridávanie detailov na povrchy modelov v PG bez nutnosti pridávania viacerých vrcholov. 

## Textúry podľa dimenzie
- 1D: pomocou jednej súradnice, gradienty
- 2D: bitmapa pixelov
- 3D: volume textures, tvorené voxelmi (3D alternatíva pixelu 1x1x1x4B) 

Môžu byť aj matematicky generované napríklad normálová textúra (z normálových vektorov).

## Textúry podľa efektu
- Difúzne: farebná hodnota na základe uhlu svetla
- Ambientné: rozptýlené svetlo bez ohľadu na polohu zdroja
- Spekulárne: odlesky
- Normálové: z normálových vektorov
- PBR: Physically Based Rendering

## Textúrovacia jednotka
Čas grafickej karty, ktorá spravuje textúry, umožňuje používať viac textúr. Môžeme priradiť rôzne textúry viacerým TU alebo na jednej TU striedať viac textúr.

Pre každú TU môžeme priradiť samplery. Samplery sú uniformné premenné v shaderi, ktoré určujú ako sa bude textúry načítať (wrapping, filtering).


```cpp
glActiveTexture(GL_TEXTURE0);  // Aktivuje texturovaciu jednotku 0
glBindTexture(GL_TEXTURE_2D, texture1);  // Naviaže textúru na jednotku

GLint samplerLoc = glGetUniformLocation(shaderProgram, "texture1");
glUniform1i(samplerLoc, 0);  

glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);

glTexImage2D(GL_TEXTURE_2D, 0, GL_RGB, width, height, 0, GL_RGB, GL_UNSIGNED_BYTE, data);
glGenerateMipmap(GL_TEXTURE_2D);
```

Pre každý fragment sa interpolujú súradnice.

```glsl
uniform sampler2D texture1;

FragColor = texture(texture1, uv)
```

### Texture wrapping
- GL_REPEAT - textúra sa opakuje (predvolené)
- GL_MIRRORED_REPEAT - textúra sa opakuje zrkadlovo
- GL_CLAMP_TO_EDGE - použije sa farba z okraja textúry
- GL_CLAMP_TO_BORDER - použije sa definovaná okrajová farba

## Mipmapy
Séria menších verzií tej istej textúry. Každá úroveň je 1/2 veľkosti predchádzajúcej. Mipmapy sa používajú zlepšenie výkonu (vykreslenie vzdialených, menších objektov) alebo na zlepšenie kvality vzdialených objektov.