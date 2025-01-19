# Z-Buffer 
Pamäť, ktorá uchováva hĺbkové informácie fragmentov. Môže sa jednať o 2D/1D pole o veľkosti displeja (1920x1080) bez Anti-Aliasingu. Z-Buffer je súčasťou Frame bufferu na GPU.

Uchováva hodnoty v závislosti od vzdialenosti od kamery. Jedná sa o hodnoty v **Normalized Device Coordinates** (-1 až 1) pretransformované vzorcom `D = (Z+1)/2` do intervalu 0.0 až 1.0.

Na začiatku sa zBuffer vyplní hodnotami 1 (nekonečno). Pre každý fragment v ZB, ak je hodnota v ZB väčšia ako súradnica Z daného fragmentu, tak sa hodnota nahradí súradnicou Z daného fragmentu.
Hodnota v Color bufferi sa nastaví na farbu fragmentu. 

```cpp
//inicializácia
for (int y = 0; y < height; ++y) {
  for (int x = 0; x < width; ++x) {
    zBuffer[y][x] = 1;
  }
}
//algoritmus
for (const auto& fragment : fragments) {
  if (zBuffer[y][x] > fragment.z) {
    zBuffer[y][x] = fragment.z;
    colorBuffer[y][x] = fragment.color;
  }
}
```

## Výhody
- Možno ho parelelizovať (pozor na súbeh)
- Rýchlejší, nemusí sa 2x iterovať každý fragment

## Nevýhody
- Vyžaduje buffer

# Maliarov algoritmus
Algoritmus radenia objektov. Vezme (min-max) interval súradníc, v ktorom sa objekt nachádza. Objekty zoradí podľa veľkosti max. Ak 2 objekty majú rovnaký maximálny interval, tak sa vezme interval min.
- Vhodný pre flat GUI

## Výhody
- Nepotrebuje buffer

## Problémy
- Cykly
- Piercing
- 2x iteruje objekty (1x pri radení a 1x pri vykreslení)

### Piercing
- Tyč - A(1,6)
- Stena - B(3,4)\
Tyč sa vykreslí ako prvá a stena ako druhá => Stena zakryje tyč, aj keď by tyč mala stenou prechádzať. 