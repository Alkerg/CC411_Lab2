# RSA y factorización de n grande
Los algoritmos y los resultados se pueden encontrar en el notebook adjunto de este repositorio [[Ver Notebook]](./algoritmos_factorizacion.ipynb)

## Algoritmo de factorización de Fermat

```python
def fermat(n):
  x = math.ceil(math.sqrt(n))
  y_2 = x**2 - n

  def is_perfect_square(z):
    return math.isqrt(z)**2 == z

  while(not is_perfect_square(y_2)):
    x += 1
    y_2 = x**2 - n

  y = math.sqrt(y_2)
  p = x + y
  q = x - y

  print(f"p = {p}, q = {q}")
```

## Algoritmo de factorización de Rabin

```python
def reduccion(n):
  y = random.randint(2, n-2)
  a = (y**2)%n
  possible_x = []

  for x in range(0,n): 
    if ((x**2)%n)%a == 0: possible_x.append(x)
  
  for x_p in possible_x:
    if x_p == 0:
      continue
    if ((y%n)%x_p != 0 and ((-y)%n)%x_p != 0):
      p = math.gcd(x_p-y,n)
      q = n/p
      print(f"p = {p}, q = {q}")
      return
```


## Resultados de benchmark con diferentes valores de N

Las pruebas se realizaron con los siguientes valores de N

```python
n_values = [21, 22275377, 72401183, 8904031, 95532967, 40053991, 165725927, 173640199, 221777863, 299526169]
```
Los resultados de las pruebas se muestran a continuación. En general el algoritmo de Rabin es mucho más lento que el algoritmo de Fermat para números grandes.

```python
N:  21
Solución mediante Fermat: 
p = 7.0, q = 3.0
Tiempo de ejecución de Fermat: 0.000022 segundos

Solución mediante Reducción: 
p = 1, q = 21.0
Tiempo de ejecución de Reducción: 0.000021 segundos

-----------------------------------------

N:  22275377
Solución mediante Fermat: 
p = 9491.0, q = 2347.0
Tiempo de ejecución de Fermat: 0.000228 segundos

Solución mediante Reducción: 
p = 9491, q = 2347.0
Tiempo de ejecución de Reducción: 1.799359 segundos

-----------------------------------------

N:  72401183
Solución mediante Fermat: 
p = 11981.0, q = 6043.0
Tiempo de ejecución de Fermat: 0.000131 segundos

Solución mediante Reducción: 
p = 11981, q = 6043.0
Tiempo de ejecución de Reducción: 5.813527 segundos

-----------------------------------------

N:  8904031
Solución mediante Fermat: 
p = 2999.0, q = 2969.0
Tiempo de ejecución de Fermat: 0.000015 segundos

Solución mediante Reducción: 
p = 2999, q = 2969.0
Tiempo de ejecución de Reducción: 0.713359 segundos

-----------------------------------------

N:  95532967
Solución mediante Fermat: 
p = 14543.0, q = 6569.0
Tiempo de ejecución de Fermat: 0.000162 segundos

Solución mediante Reducción: 
p = 1, q = 95532967.0
Tiempo de ejecución de Reducción: 8.194139 segundos

-----------------------------------------

N:  40053991
Solución mediante Fermat: 
p = 19997.0, q = 2003.0
Tiempo de ejecución de Fermat: 0.000735 segundos

Solución mediante Reducción: 
p = 2003, q = 19997.0
Tiempo de ejecución de Reducción: 3.219784 segundos

-----------------------------------------

N:  165725927
Solución mediante Fermat: 
p = 16561.0, q = 10007.0
Tiempo de ejecución de Fermat: 0.000090 segundos

Solución mediante Reducción: 
p = 16561, q = 10007.0
Tiempo de ejecución de Reducción: 14.512980 segundos

-----------------------------------------

N:  173640199
Solución mediante Fermat: 
p = 19373.0, q = 8963.0
Tiempo de ejecución de Fermat: 0.000194 segundos

Solución mediante Reducción: 
p = 8963, q = 19373.0
Tiempo de ejecución de Reducción: 14.529644 segundos

-----------------------------------------

N:  221777863
Solución mediante Fermat: 
p = 19853.0, q = 11171.0
Tiempo de ejecución de Fermat: 0.000135 segundos

Solución mediante Reducción: 
p = 11171, q = 19853.0
Tiempo de ejecución de Reducción: 18.959383 segundos

-----------------------------------------

N:  299526169
Solución mediante Fermat: 
p = 19333.0, q = 15493.0
Tiempo de ejecución de Fermat: 0.000047 segundos

Solución mediante Reducción: 
p = 1, q = 299526169.0
Tiempo de ejecución de Reducción: 25.174262 segundos

-----------------------------------------
```