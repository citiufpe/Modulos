## Modulos iOS

**Autor**: Eduardo Leite

**Contato**: eduardo.leite@citi.ufpe.br

**Git**: eduardolsneto2

1. Get e Post Request:

    GET: Usando Closures (Recomendado)

    Adicione na sua Classe de comunicação com o servidor(nesse exemplo será 'ServerCom'):

    Uso da função:

    ```swift
    //teste
    let url = "url do request"
    ServerCom.httpRequest(urlString: url ,callback: {(result:[String:Any], error: NSError?) -> () in
    // Callback aqui
    })
    ```
    
    
