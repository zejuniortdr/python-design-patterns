# Factory

O termo *factory* refere-se a uma classe responsável por criar objetos de outros tipos.

Vantagens em se utilizar este padrão:
- Baixo acoplamento. A criação de um objeto pode ser independente da implementação da classe;
- O cliente não precisa conhecer a classe que cria o objeto, basta conhecer a interface, os métodos e parâmetros que devem ser passados para criação do objeto, o que simplifica a implementação;
- Adicionar outra classe à fábrica para criar objetos de outro tipo pode ser facilmente implementado sem que o cliente altere o código. No mínimo exigirá a passagem de outro parâmetro;
- Reutilização de objetos existentes. 

Existem três variantes do padrão *Factory*
- *Simple Factory*: Permite que as interfaces criam objetos sem expor a lógica de sua criação;
- *Factory Method*: Permite que as interfaces criem objetos, mas adia a decisão para que as subclasses determinem a classe para criação de objetos;
- *Abstract Factory*: Uma Abstract Factory é uma interface padra cria objetos relacionados sem especificar/expor suas classes; O padrão fornece objetos de outra fábrica que internamente cria outros objetos;

## Simple Factory

Este padrão é o a classe mais simples que possui os métodos para a criação de instâncias de classes.
Muitos desenvolvedores consideram nem consideram este como um padrão, mas sim um conceito.

Um exemplo em python deste conceito/padrão, poderia ser:

```python
from abc import ABCMeta, abstractmethod

class Animal(metaclass=ABCMeta):
    @abstractmethod
    def do_say(self):
        pass
    

class Dog(Animal):
    def do_say(self):
        print("AU AU!")
    

class Cat(Animal):
    def do_say(self):
        print("Meow Meow!")
    
# fábrica forest definida
class ForestFactory(object):
    def make_sound(self, object_type):
        return eval(object_type)().do_say()


# código do cliente
if __name__ == "__main__":
    ff = ForestFactory()
    animal = input("Which animal shoul make_sound? Dog or Cat? ")
    ff.make_sound(animal)
    
```

E como saída teríamos:
```
Which animal shoul make_sound? Dog or Cat? Dog
AU AU!
```