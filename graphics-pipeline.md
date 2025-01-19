# Vykresľovací reťazec / Graphics Pipeline

![pipeline](assets/graphics-pipeline.png)

## Data

```cpp
const float data[] = {
    //vrchol, normála, uv souřadnice
    1.0f, 0.0f, 1.0f,   0.0f, 1.0f, 0.0f,   0.0f, 0.0f,
    1.0f, 0.0f,-1.0f,   0.0f, 1.0f, 0.0f,   10.0f, 0.0f,
   -1.0f, 0.0f,-1.0f,   0.0f, 1.0f, 0.0f,   10.0f, 10.0f,
 
   -1.0f, 0.0f, 1.0f,   0.0f, 1.0f, 0.0f,   0.0f, 10.0f,
    1.0f, 0.0f, 1.0f,   0.0f, 1.0f, 0.0f,   0.0f, 0.0f,
   -1.0f, 0.0f,-1.0f,   0.0f, 1.0f, 0.0f,   10.0f, 10.0f
};
```
Vytvoríme identifikátory **Vertex Buffer Object** (VBO) a **Verter Array Object** (VAO). Nahráme dáta do array bufferu GPU a buffer priradíme k VBO. 

`glDrawArrays(GL_TRIANGLES, 0, 6);` spustí pipeline.

## Vertex Shader
Každý vrchol prejde vertex shaderom. Výstup je:
```glsl
ex_worldPos = modelM * vec4(vp, 1.0);
mat4 normal = transpose(inverse(modelM));
ex_worldNorm = vec3(normal * vec4(vn, 1.0));

gl_Position = projectM * viewM * modelM * vec4(vp, 1.0);
```
Po vynásobení sa vrchol nachádza v:
1. modelM: world space
2. viewM: view space
3. projectM: clip space

## Clipping
