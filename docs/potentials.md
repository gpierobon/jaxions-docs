---
layout: default
title: Potentials
parent: Physics
nav_order: 2
---

$$
V = V(\vert\phi\vert)+V(\theta)
$$

Radial part of the potential

| Flag       | Form           | 
|:-------------|:------------------|
| **default**  | $$V(\vert\phi\vert)=\frac{\lambda}{4}(\vert\phi\vert^2-v^2)^2$$ |
| `--vpq2` | $$V(\vert\phi\vert)=\frac{\lambda}{16}(\vert\phi\vert^4-v^4)^2$$ |

Angular part of the potential

| Flag       | Form           | 
|:-------------|:------------------|
| **default**  | $$V(\theta)=\chi\left(1-{\rm Re}\frac{\phi}{v}\right)$$ |
| `--vqcdC` | $$V(\theta)=\chi(1-\cos\theta)$$ |
| `--vqcdV` | $$V(\theta)=\frac{\chi}{2}\left[\left((1-{\rm Re}\frac{\phi}{v}\right)^2+\left({\rm Im}\frac{\phi}{v}\right)^2\right]^2$$ |
| `--vqcdL --beta <beta>` | $$V(\theta)=\chi\left(\frac{1}{2}\theta^2-\frac{\beta^2}{24}\theta^3\right)$$ |

Under construction ...
