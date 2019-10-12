# imagemagick

## Reduzindo a qualidade da imagem em 50%

```text
mogrify -strip -quality 50% -type optimize -format jpg *
```

## Conversão de imagens em lote \(PNG para JPG\)

```text
mogrify -format jpg *.png
```

