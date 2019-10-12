# awk

## Remoção de linhas em branco

```text
awk 'NF>0' arquivo.txt
```

## **Remover strings duplicadas de um arquivo**

```text
 $ awk '{for(i=1;i<=NF;i++) a[$i]++} END{for(i in a) printf i" ";print ""}' arquivo.txt
```

