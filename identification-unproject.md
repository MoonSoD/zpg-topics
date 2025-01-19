# Identifikácia
Proces, ktorým identifikujeme objekty, na ktoré užívateľ klikol.

## Stencil buffer
Rozšírenie Z-Bufferu, pamäť, kde každý pixel má 8 bitovú hodnotu. Je fyzicky uložený spolu s Z-Bufferom. Volá sa po rasterizácii, depth teste a pred fragment shaderom.

```cpp
glEnable(GL_STENCIL_TEST);
glStencilOp(GL_KEEP, GL_KEEP, GL_REPLACE); // možné operácie (stencil fail, depth fail, both pass)
glStencilFunc(GL_ALWAYS, 1, 0xFF); // porovnávacia funkcia, 
// 0xFF, 
// Ox0F pre 00001111, 
// 0xF0 pre 11110000

//GL_EQUAL, GL_NOTEQUAL, GL_LESS, GL_LEQUAL, GL_GREATER, GL_GEQUAL, GL_ALWAYS
```

### Stencil test
- Pre každý fragment sa vykoná stencil test.
- Porovná sa hodnota fragmentu v stencil bufferi s referenčnou hodnotou zadanej vo funkcii. \
`(REF & MASK cmp VAL_IN_BUFFER & MASK)`
- Musí vrátiť 1, aby bol test úspešný.
- Podľa `glStencilOp` sa vykoná operácia na testovanom fragmente.

#### K čomu je tam maska?
Maska určuje, ktoré bity hodnôt sa majú porovnať s referenčnou hodnotou. Môžeme napríklad uložiť do prvý 4 bitov ID, do druhých 4 bitov nejakú inú hodnotu.

### Čítanie stencil bufferu
```cpp
glReadPixels(x, y, 1, 1, GL_STENCIL_INDEX, GL_UNSIGNED_INT, &index);
```

# Unproject
Prevádza 2D bod na obrazovke na 3D bod vo world space. Jedná sa o inverzný proces k projekcii.

### V OpenGL

```cpp
GLfloat depth;
glReadPixels(x, y, 1, 1, GL_DEPTH_COMPONENT, GL_FLOAT, &depth);

glm::vec4 viewport = glm::vec4(0, 0, frameWidth, frameHeight);
glm::vec3 windowCoords = glm::vec3(x, y, depth);

glm::vec3 p = glm::unProject(windowCoords, viewMatrix, projectionMatrix, viewport);
```

### Matematicky
```
NDC_x = (2.0 * screen_x) / viewport_width - 1.0
NDC_y = (2.0 * screen_y) / viewport_height - 1.0
NDC_z = 2.0 * zbuffer_z - 1.0

[NDC_x, NDC_y, NDC_z, 1.0] * inverse(projectionMatrix * viewMatrix)
```