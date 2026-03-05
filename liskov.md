Introduzido por Barbara Liskov, sua definição formal diz que:

> “Se para cada objeto o1 do tipo S há um objeto o2 do tipo T de forma que, para todos os programas P definidos em termos de T, o comportamento de P é inalterado quando o1 é substituído por o2 então S é um subtipo de T”.

Em outras palavras, o princípio define que os objetos de uma superclasse devem ser substituíveis por objetos de suas subclasses sem quebrar a aplicação. Isso exige que os objetos de suas subclasses se comportem da mesma maneira que os objetos de sua superclasse.

Um método substituído de uma subclasse precisa aceitar os mesmos valores de parâmetros de entrada que o método da superclasse. Isso significa que você pode implementar regras de validação menos restritivas, mas não tem permissão para impor regras mais rigorosas em sua subclasse. Caso contrário, qualquer código que chame esse método em um objeto da superclasse pode causar uma exceção, se for chamado com um objeto da subclasse.

Regras semelhantes se aplicam ao valor de retorno do método. O valor de retorno de um método da subclasse precisa estar em conformidade com as mesmas regras que o valor de retorno do método da superclasse. Você só pode decidir aplicar regras ainda mais rígidas retornando uma subclasse específica do valor de retorno definido ou retornando um subconjunto dos valores de retorno válidos da superclasse.

Para aplicar esse princípio ao código, o comportamento das classes se tornará mais importante do que sua estrutura. Infelizmente, não existe uma forma fácil de fazer cumprir este princípio. É preciso implementar verificações próprias para garantir que o código siga o Princípio de Substituição de Liskov. Na melhor das hipóteses, por meio de revisões de código e casos de teste.

Nos casos de teste, pode-se executar uma parte específica da aplicação com objetos de todas as subclasses para garantir que nenhum deles cause um erro ou altere significativamente o desempenho, mas ainda mais importante é garantir que todos os casos de teste necessários foram criados e executados.

Quando esse princípio é ignorado, cria-se relações de herança frágeis e inconsistentes, que causam falhas inesperadas, dificultam a manutenção e comprometem a confiabilidade do código.

## Consequências de ignorar o princípio

Algumas das principais consequências incluem:

- **Comportamento inesperado em tempo de execução:** métodos sobrescritos podem introduzir exceções, retornar valores diferentes ou alterar regras de negócio de forma silenciosa.
- **Testes quebrando sem motivo aparente:** um teste que passa para a superclasse pode falhar para a subclasse, mesmo que o código pareça estar “correto”.
- **Contratos violados:** se um código depende de um comportamento específico da superclasse, e a subclasse o ignora ou altera, o sistema perde consistência.
- **Herança mal utilizada:** subclasses que “quebram” o funcionamento esperado são um sinal claro de que talvez o relacionamento de herança não deva existir.

Esses problemas tornam o sistema difícil de evoluir, e o uso de herança — que deveria trazer reutilização e flexibilidade — acaba sendo fonte de bugs difíceis de identificar e resolver.

## Sinais comuns de violação do Liskov Substitution Principle

- **Sobrescritas que lançam exceções onde a superclasse não lançaria:** subclasses que “quebram” funcionalidades esperadas da classe base.
- **Métodos sobrescritos com comportamento diferente:** a subclasse altera o resultado, lógica ou efeitos colaterais de um método da superclasse, confundindo quem usa a classe base.
- **Necessidade de verificações com `instanceof` ou `typeof`:** se o código precisa saber “qual subclasse está sendo usada” para funcionar corretamente, é sinal de que a substituição não é transparente.
- **Testes que passam para a superclasse, mas falham para a subclasse:** indica que a subclasse não respeita o mesmo contrato esperado.
- **Herdar apenas por reuso de código:** subclasses que não representam um real “é um” da superclasse costumam gerar substituições problemáticas.

## Como evitar a violação do LSP

Para não violar o **Liskov Substitution Principle**, além de estruturar muito bem a aplicação com boas abstrações, em alguns casos será necessário usar **injeção de dependência**, assim como outros princípios do **SOLID**, como:

- **OCP (Open/Closed Principle)**
- **ISP (Interface Segregation Principle)**

Seguir o LSP permite usar o **polimorfismo** com mais confiança. Assim, é possível chamar classes derivadas referindo-se à sua classe base sem preocupações com resultados inesperados.
