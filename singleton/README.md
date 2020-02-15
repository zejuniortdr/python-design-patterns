# Singleton

O padrão *Singleton* proporciona uma forma de ter um e somente um objeto de determinado tipo além de disponibilizar um ponto de acesso global.
Este padrão normalmente é usado em casos como logging, operações de banco de dados spollers de impressão, e em vários outros cenários onde é necessário garantir que exista somente uma instância disponível para toda a aplicação, para evitar requisições conflitantes para o mesmo recurso.

## E como podemos implementar esse padrão em python?

Existem duas formas:
    1. Sobrescrever o método `__new__` da classe;
    2. Utilizar *lazy initialization*;


### Sobrescrever o `__new__`:
Um exemplo de como o padrão Singleton pode ser implementado em python: 

```python
class Singleton(object):
    def __new__(cls):
        if not hasattr(cls, 'instance'):
            cls.instance = super(Singleton, cls).__new__(cls)
        return cls.instance


s = Singleton()
print("Objeto criado: ", s)

s1 = Singleton()
print("Objeto criado: ", s1)
```

E como saída, teríamos:

```
Objeto criado:  <__main__.Singleton object at 0x105a48dd0>
Objeto criado:  <__main__.Singleton object at 0x105a48dd0>
```

Repare que o mesmo objeto é retornado tanto para `s` quanto para `s1`. Na segunda invocação do construtor, é identificado que `Singleton` já possui uma instância criada, e para este caso simplesmente retorna o mesmo objeto.


### Lazy initialization 

Quando é necessário uma inicialização "preguiçosa", o objeto não é criado no instante que é invocado, mas somente no instante que se fizer necessário. Isso garante que seja possível otimizar recursos.

Um exemplo de como o padrão Singleton com `Lazy initialization ` pode ser implementado em python: 

```python
class Singleton(object):
    __instance = None

    def __init__(self):
        if not Singleton.__instance:
            print("__init method called")
        else:
            print("Instance alredy created:", self.get_instance())    

    @classmethod
    def get_instance(cls):
        if not cls.__instance:
            cls.__instance = Singleton()
        return cls.__instance


s = Singleton() # classe inicializada, mas o objeto não será criado
print("Objeto criado: ", Singleton.get_instance()) # objeto é criado aqui

s1 = Singleton() # instância já criada
print(s1)
```