# Factory Method

## Definição do GoF, no livro "Padrões de Projeto" (2000)

### Intenção: 
Definir uma interface para criar um objeto, mas deixar as subclasses decidirem que classe instanciar. O Factory Method 
permite adiar a instanciação para subclasses.

### Tipo de pattern:
Criação

### Também conhecido como:
Virtual Constructor

### Aplicável quando:
- Uma classe não pode antecipar a classe de objetos que deve criar.
- Uma classe quer que suas subclasses especifiquem os objetos que criam.
- Classes delegam responsabilidade para uma dentre várias subclasses auxiliares, e você quer localizar o conhecimento de
qual subclasse auxiliaar que é a delegada.

### Participantes:
- **Product:** Define a interface de objetos que o **FactoryMethod** cria.
- **ConcreteProduct:** Implementa a interface de **Product**
- **Creator:** Declara o **FactoryMethod**, o qual retorna um objeto do tipo **Product**. **Creator** pode também 
definir uma implementação por omissão do **FactoryMethod**, que retorna por omissão um objeto **ConcreteProduct**. Pode chamar o 
**FactoryMethod** para criar um objeto **Product**
- **ConcreteCreator:** Redefine o **FactoryMethod** para retornar uma instância de um **ConcreteProduct**