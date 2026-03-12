O Princípio de Substituição de Liskov (liskov substitution principle, ou LSP no inglês) foi introduzido pela cientista da computação Barbara Liskov em 1987 durante a conferência OOPSLA (Object-Oriented Programming, Systems, Languages, and Applications). Mas foi em 1994 que ela definiu a base teórica do conceito no Artigo "A Behavioral Notion of Subtyping", escrito em parceria com a cientista da computação Jeannette Wing. No artigo elas criam a definição formal diz que: “Se para cada objeto o1 do tipo S há um objeto o2 do tipo T de forma que, para todos os programas P definidos em termos de T, o comportamento de P é inalterado quando o1 é substituído por o2 então S é um subtipo de T”. 
Em outras palavras, o princípio define que os objetos de uma superclasse devem ser substituíveis por objetos de suas subclasses sem quebrar o funcionamento da  aplicação. Isso exige que os objetos de suas subclasses se comportem da mesma maneira que os objetos de sua superclasse.

Além dessa definição de substituição estrutural, o LSP tem algumas regras sobre o comportamento dos métodos:  Um método substituído de uma subclasse precisa aceitar os mesmos valores de parâmetros de entrada que o método da superclasse. Isso significa que é possível implementar regras de validação menos restritivas, porém nunca mais rigorosas. Caso contrário, qualquer código que chame esse método em um objeto da superclasse pode causar uma exceção, se for chamado com um objeto da subclasse. O que violaria todo o princípio de transparência de substituição. 
Podemos utilizar o mesmo raciocínio no método devolve. Pois o valor de retorno de uma subclasse deve sempre estar em conformidade com as mesmas regras com as mesmas regras que o valor de retorno do método proveniente da superclasse. 
Na prática do dia a dia, o programador pode até ser mais específico no que entrega. Sendo assim é válido retornar um subtipo mais especializado ou um subconjunto restrito de valores válidos. Porém nunca pode ser algo que a classe não previu. Podemos exemplificar da seguinte forma: se um método pai prometeu entregar um ‘Veículo’, o filho pode entregar um ‘Carro’ (que é um veículo específico).  Mas o que ele jamais deve fazer é entregar algo que fuja daquilo que a superclasse definiu. Pois isso causaria exceções inesperadas para quem chamou este método.


Para aplicar esse princípio em um sistema, o comportamento das classes especificamente se tornam mais relevantes do que a sua estrutura puramente técnica. Infelizmente, não existe nenhuma forma simplificada, nenhuma ferramenta automatizada que force o cumprimento do LSP. Para aplicar é preciso utilizar processos manuais, como revisões do código detalhadas e ter uma estratégia sólida e comprovada para realizar testes eficientes. E a prática de testes recomendada, quando se utiliza LSP é a execução de partes críticas da aplicação utilizando objetos de diferentes subclasses, para garantir que nenhuma das partes cause exceções inesperadas ou afete o desempenho da aplicação negativamente. Além de simplesmente testar, é preciso assegurar que os cenários de testes sejam abrangentes o suficiente, de forma que valide o comportamento das subclasses.


Quando os desenvolvedores ignoram o princípio de Liskov o resultado é um código que possui relações de heranças frágeis e inconsistentes. O que acaba gerando falhas inesperadas, afeta a manutenibilidade  e compromete a confiança com o código. 
Algumas das principais consequências  de não considerar as regras do LSP incluem: 
Comportamento inesperado em tempo de execução: Métodos sobrescritos podem introduzir exceções não previstas, retornar valores fora do esperado ou alterar regras de negócio de forma silenciosa.
Testes quebrando sem motivo aparente: Um cenário de teste que é executado corretamente para a superclasse pode falhar para a subclasse, mesmo que a sintaxe pareça certa. 
Violação dos contratos: Se o código depende de um comportamento específico da superclasse, e a subclasse o ignora ou altera, o sistema perde toda a sua integridade semântica 
Herança Indevida: Quando as subclasses quebram o funcionamento esperado isso demonstra que aquele relacionamento de herança específico talvez não devesse existir
Esses problemas criam um sistema que é difícil de evoluir, tanto para expandir as funcionalidades ou garantir a manutenção a longo prazo. Dessa forma, o uso de herança, que deveria trazer reutilização e flexibilidade, acaba sendo fonte de bugs difíceis de identificar e resolver.


Os sinais comuns de violação do Liskov Substitution são: 

-Sobrescritas que acabam lançando exceções inesperadas: Quando a subclasse lança uma exceção, em um cenário onde a superclasse não lançaria, o que gera comportamentos inesperados.

-Comportamentos divergentes: A subclasse altera toda a lógica, os resultados ou efeitos colaterais de um método, o que acaba por confundir quem utiliza a classe base.

-Uso excessivo de  instanceof ou typeof: Se o código precisa verificar sempre qual a subclasse em específico que faz funcionar, então a substituição não é transparente para o programa.

-Inconsistência nos cenários de testes: Quando os testes  da classe base falham em algumas das subclasses há uma forte indicação que o contrato foi desrespeitado.

-Herança por conveniência: Problema que surge quando se utiliza a herança apenas para reaproveitar o código, sem que exista uma relação clara entre eles, que ocorre quando não podemos afirmar que a subclasse “é um” da superclasse. Essa prática torna a herança problemática, pois a substituição deixa de ser segura e transparente.


Para não violar o Liskov Substitution Principle (LSP), além de projetar boas abstrações, é fundamental integrar outras práticas do SOLID, que acabam funcionando em conjunto. Especialmente o OCP (princípio Aberto/Fechado) e o ISO (princípio da segregação da interface), os quais são comumente apoiados pela Injeção Dependência. Quando se adere ao LSP é possível explorar o conceito de polimorfismo com total confiança, e assim, se torna possível interagir com as classes derivadas por meio de suas superclasses, sem ter o receio de se deparar com comportamentos imprevisíveis ou falhas colaterais. 

Para aplicar o Princípio de Substituição de Liskov de uma forma mais eficiente, uma boa solução é usar o conceito de Design por Contrato. Em vez de apenas herdar código para reaproveitá-lo, o desenvolvedor precisa garantir que a subclasse cumpra todas as promessas feitas pela superclasse. São três passos principais nesse processo: primeiro, fazer um refinamento das abstrações, ou seja, dividir hierarquias muito genéricas em interfaces ou classes menores e mais específicas. Por exemplo, separar veículos motorizados de veículos manuais. Depois, é importante manter as pré-condições, assegurando que a subclasse não exija mais do que a classe pai. E, por fim, preservar as pós-condições, garantindo que o retorno dos métodos e seus efeitos colaterais continuem compatíveis. Quando a substituição parecer forçada ou difícil de encaixar, vale a pena optar pela composição ao invés da herança.

---

Analogia com o Mundo Real utilizando Veículos

Imagine uma empresa que faz transporte de pessoas,  onde a classe chamada veículo é criada. Nesta classe é definido os comportamentos de acelerar, frear e transportar pessoas. nesta criamos as subclasses Carro, Moto e ônibus, todas vão funcionar corretamente, pois no cenário de exemplo: “pegue veículo e leve pessoas até o destino”  a classe pode estar se referindo a carro, moto ou ônibus. Neste caso, a analogia respeita o princípio de liskov. Mas se caso seja adicionado um novo veículo não motorizado, por exemplo bicicleta, na subclasse Veículo motorizado onde classe possui Ligar_motor() e acelerar(), a bicicleta não possuindo motor teria que ignorar ligar_motor() ou lançar erro. Para não quebrar o princípio de liskov, vamos criar uma outra classe chamada veículos não motorizados onde esta pode resolver o princípio de liskov e além disso respeita o princípio de aberto e fechado.

---
Exemplo de codigo Utilizando Java

abstract class Veiculo {
    public abstract void mover();
}

abstract class VeiculoMotorizado extends Veiculo {
    public abstract void ligarMotor();
}

abstract class VeiculoNaoMotorizado extends Veiculo {
    public abstract void pedalar();
}

class Carro extends VeiculoMotorizado {

    @Override
    public void ligarMotor() {
        System.out.println("Motor do carro ligado.");
    }

    @Override
    public void mover() {
        System.out.println("O carro está se movendo.");
    }
}

class Moto extends VeiculoMotorizado {

    @Override
    public void ligarMotor() {
        System.out.println("Motor da moto ligado.");
    }

    @Override
    public void mover() {
        System.out.println("A moto está se movendo.");
    }
}

class Bicicleta extends VeiculoNaoMotorizado {

    @Override
    public void pedalar() {
        System.out.println("Pedalando a bicicleta.");
    }

    @Override
    public void mover() {
        System.out.println("A bicicleta está se movendo.");
    }
}

public class Main {
    public static void main(String[] args) {

        VeiculoMotorizado carro = new Carro();
        carro.ligarMotor();
        carro.mover();

        VeiculoMotorizado moto = new Moto();
        moto.ligarMotor();
        moto.mover();

        VeiculoNaoMotorizado bicicleta = new Bicicleta();
        bicicleta.pedalar();
        bicicleta.mover();
    }
}

Exemplo de codigo utilizando python

from abc import ABC, abstractmethod

class Veiculo(ABC):
	
	 @abstractmethod
	  def mover(self):
	   pass
	 
	 
	 class VeiculoMotorizado(Veiculo):
	 
	 @abstractmethod
	  def ligar_motor(self):
	   pass
	 
	 
	 class VeiculoNaoMotorizado(Veiculo):
	 
	 @abstractmethod
	  def pedalar(self):
	   pass
	 
	 
	 class Carro(VeiculoMotorizado):
	 
	 def ligar_motor(self):
	  print("Motor do carro ligado")
	 
	 def mover(self):
	  print("O carro está se movendo")
	 
	 
	 class Moto(VeiculoMotorizado):
	 
	  def ligar_motor(self):
	   print("Motor da moto ligado")
	 
	  def mover(self):
	   print("A moto está se movendo")
	 
	 
	 class Bicicleta(VeiculoNaoMotorizado):
	 
	  def pedalar(self):
	   print("Pedalando a bicicleta")
	 
	  def mover(self):
	   print("A bicicleta está se movendo")
	 
	 
	 carro = Carro()
	 carro.ligar_motor()
	 carro.mover()
	 
	 moto = Moto()
	 moto.ligar_motor()
	 moto.mover()
	 
	 bike = Bicicleta()
	 bike.pedalar()
	 bike.mover()

---
Referências

https://medium.com/@tbaragao/solid-l-s-p-liskov-substitution-principle-3a31c3a7b49e

https://vinicius-sanchez.medium.com/solid-liskov-substitution-principle-lsp-d70297367d03

https://stackify.com/solid-design-liskov-substitution-principle/

https://blog.formacao.dev/l-de-solid-substituicoes-sem-surpresas-com-o-principio-de-liskov/



