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
definir uma implementação por omissão do **FactoryMethod**, que retorna por omissão um objeto **ConcreteProduct**. 
Pode chamar o **FactoryMethod** para criar um objeto **Product**
- **ConcreteCreator:** Redefine o **FactoryMethod** para retornar uma instância de um **ConcreteProduct**

### Oportunidades:
#### Segregar lógicas complexas do código:
 **FactoryMethod** ajudam na segregação de lógicas complexas, atribuindo a
responsabilidade para métodos mais específicos, tornando a interface de exposição mais simples e limpa, deixando para a
implementação de cada interface a aplicação correta da lógica, conforme escopo.

Ex: Ao invés de manter uma regra de serialização de retorno (JSON, XML, etc) na camada de service, pode-se deixar para a 
implementação da **FactoryMethod** tomar a decisão do tipo de serialização conforme serialização requerida:

- Sem usar uma **FactoryMethod**
```python
class response_serializer:
    def json_serializer(self, resp):
        payload = {
            "body" : resp.body()
        }  
        return json.dumps(payload)

    def xml_serializer(self, resp):
        resp_element = et.Element("body", attrib={"body":resp.body})
        return et.tostring(resp_element, encoding="UTF-8")

class client_serializer:
    if __name__ == "__main__":
        # Mocking call
        response = api.get()
        serializer = response_serializer()
        
        if return_type is "JSON":
            return response_serializer.json_serializer(response)
        elif return_type is "XML":
            return response_serializer.json_serializer(response)
        # Other formats
```

- Usando uma **FactoryMethod**

```python
class response_serializer:
    def serializer(self, resp, format):
        if format is "JSON":
            return _json_serializer(resp)
        elif format is "XML":
            return _xml_serializer(resp)
        # Other formats

    def _json_serializer(self, resp):
        payload = {
            "body" : resp.body()
        }  
        return json.dumps(payload)
    def _xml_serializer(self, resp):
        resp_element = et.Element("body", attrib={"body":resp.body})
        return et.tostring(resp_element, encoding="UTF-8")

class client_serializer:
    if __name__ == "__main__":
        # Mocking call
        serializer = response_serializer()
        response = api.get()
        return serializer.serializer(response, return_type)       
```