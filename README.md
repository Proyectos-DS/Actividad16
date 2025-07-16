# Actividad 16: Práctica del ciclo TDD


## Ejercicios

### Incrementar un contador (ruta dedicada)

Prueba implementada , siguiendo la guía. Ejecución:

```sh
test_counter.py::test_increment_counter PASSED                                                             [100%]

=============================================== 6 passed in 0.41s ================================================
(.venv) dirac@ubuntu:~/Documents/DS/Actividad16/practica_tdd$ 
```

### Establecer valor específico

Al código brindado en la guía le falto especificar la importación de `request`, ya que se usa en este método:

```python
@app.route("/counters/<name>/set", methods=["PUT"])
@require_counter
def set_counter(name):
    body = request.get_json()
    COUNTERS[name] = body.get("value", COUNTERS[name])
    return {name: COUNTERS[name]}, status.HTTP_200_OK
```

Las pruebas fueron exitosas:

```sh
test_counter.py::test_create_a_counter PASSED                                                              [ 14%]
test_counter.py::test_duplicate_counter PASSED                                                             [ 28%]
test_counter.py::test_update_counter PASSED                                                                [ 42%]
test_counter.py::test_read_counter PASSED                                                                  [ 57%]
test_counter.py::test_delete_counter PASSED                                                                [ 71%]
test_counter.py::test_increment_counter PASSED                                                             [ 85%]
test_counter.py::test_set_counter PASSED                                                                   [100%]

=============================================== 7 passed in 0.43s ================================================
(.venv) dirac@ubuntu:~/Documents/DS/Actividad16/practica_tdd$ ^C
(.venv) dirac@ubuntu:~/Documents/DS/Actividad16/practica_tdd$ 
```

### Listar todos los contadores

Para este ejercicio se registran dos nuevos contadores `a` y `b`, estos se guardan en el diccionario `COUNTERS`. Luego se llama al método `client.get("/counters")` que se define en la implementación **green**:

```python
@app.route("/counters", methods=["GET"])
def list_counters():
    return COUNTERS, status.HTTP_200_OK
```

El diccionario devuelto sería `{"a": 0, "b": 0}`.

### Reiniciar un contador

- **Para la prueba**: se crea un nuevo contador `tmp` con `POST` y luego se actualiza con `PUT` por lo que el contador debe estar en 1. Al llamar a `/counters/tmp/reset` el contador debería volver a 0.
- **Para la implementación**: se define una nueva ruta `/counters/<name>/reset` a la cual si se accede con el mpetodo `PUT` resetea el contador `<name>` a 0.

### Ejecución final

```sh
(.venv) dirac@ubuntu:~/Documents/DS/Actividad16/practica_tdd$ pytest -v
============================================== test session starts ===============================================
platform linux -- Python 3.12.3, pytest-8.4.1, pluggy-1.6.0 -- /home/dirac/Documents/DS/Actividad16/practica_tdd/.venv/bin/python
cachedir: .pytest_cache
rootdir: /home/dirac/Documents/DS/Actividad16/practica_tdd
plugins: cov-6.2.1
collected 9 items                                                                                                

test_counter.py::test_create_a_counter PASSED                                                              [ 11%]
test_counter.py::test_duplicate_counter PASSED                                                             [ 22%]
test_counter.py::test_update_counter PASSED                                                                [ 33%]
test_counter.py::test_read_counter PASSED                                                                  [ 44%]
test_counter.py::test_delete_counter PASSED                                                                [ 55%]
test_counter.py::test_increment_counter PASSED                                                             [ 66%]
test_counter.py::test_set_counter PASSED                                                                   [ 77%]
test_counter.py::test_list_counters PASSED                                                                 [ 88%]
test_counter.py::test_reset_counter PASSED                                                                 [100%]

=============================================== 9 passed in 0.72s ================================================
(.venv) dirac@ubuntu:~/Documents/DS/Actividad16/practica_tdd$ 
```