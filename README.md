# Entrega 9 
Para la entrega 9 se cumplieron todos los puntos aplicando los cambios sobre la página "Novedades".

## Mixin

Como mixin declare una funcion llamada Size, la cual es utilizada en mi archivo novedades.scss para cambiar los tamaños de los componentes en base a los argumentos. 

```scss
@mixin sizes($width, $height) {
  height: $height;
  width: $width;
}
```


## Map

Como map declare dos elementos:

### lugares


```scss
$lugares:(
  cerro-7colores: #4d2b39,
  garganta-del-diablo: #5acbe7,
  salinas: #b2dd14,
  hornocal: #20bf55
  );
```
Este map se utilizo para darle estilo a las cajas que contiene cada uno de los lugares. El estilo se aplico a los bordes cuando se hace el hover y al color de fondo de la descripcion. 


```scss
  &__tarjeta {
    @include sizes(100%, 90%);
    &__img {
      @include sizes(100%, 80%);
      
      @each $lugar, $color in $lugares {
        &##{$lugar}:hover {
          transform: scale(1.5, 1.5);
          border: 8px solid $color; 
        }
      }
    }

...

}
```

```scss

{
    ...

 &__descripcion {
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      font-size: 18px;
      font-weight: bold;
      background-color: $claro;
      height: 45px;

      
    @each $lugar, $color in $lugares{

      &-#{$lugar} {
        @extend .novedades__tarjeta__descripcion ;
        background-color: $color;
      }

    }

    }



  }


```



### fuentes

```scss
$fuentes:(
  titulo: (color: $principal, tamaño: 64px),
  subtitulos: (color: $oscuro, tamaño: 24px),
  texto: (color: $principal, tamaño:18px),
);
```

Este map se utilizo para aplicar diferentes estilos al texto de la página Novedades. Usando un Map Get se aplico el estilo individual en cada elemento.

```scss
.accordion-collapse.collapse {
  font-size: map-get($fuentes, texto, tamaño);
}
```

```scss
.novedades {
  &__titulo {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 80px;
    background-color: $claro;
    font-size: map-get($fuentes, subtitulos, tamaño);
    color: map-get($fuentes, subtitulos, color );
```
```scss
 &__titulo {
    @include sizes(100%, 100%);

    color: map-get($fuentes , titulo, color );

    font-size: map-get($fuentes , titulo, tamaño );
    font-weight: bold;
    text-align: center;

    margin-top: 40px;
```
## Extend
Se utilizo el extend para aplicar diferentes estilos sobre las descripciones de los lugares. Por una cuestion de facilidad lo hice mediante un Map para aprovechar las ventajas que ofrece.
```scss
    &__descripcion {
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      font-size: 18px;
      font-weight: bold;
      background-color: $claro;
      height: 45px;

      
    @each $lugar, $color in $lugares{

      &-#{$lugar} {
        @extend .novedades__tarjeta__descripcion ;
        background-color: $color;
      }

    }

    }



```
Cada vez que se itera sobre los elementos del Map Lugares se genera una clase llamada "novedades__tarjeta__descripcion-$lugar" la cual hereda todos los estilos de la clase "novedades__tarjeta__descripcion".
