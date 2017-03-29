## Modulos iOS

**Autor**: Eduardo Leite

**Contato**: eduardo.leite@citi.ufpe.br

**Git**: eduardolsneto2

1. Get e Post Request:

    GET: Usando Closures (Recomendado)

    Adicione na sua Classe de comunicação com o servidor(nesse exemplo será 'ServerCom'):

    ```swift
    class func httpRequest(urlString:String, callback:@escaping (_ result: [String:Any],_ error: NSError?) -> ()){
        let url = NSURL(string: urlString)
        let task = URLSession.shared.dataTask(with: url! as URL) {(data, response, error) in
            do{
                if let data = data,
                    let json = try JSONSerialization.jsonObject(with: data) as? [String:Any]{
                    callback(json,error as NSError?)
                }
            } catch {
                print("Error deserializing JSON: \(error)")
            }
        }//finishing the http request
        task.resume()
    }
    ```

    Uso da função:

    ```swift
    let url = "url do request"
    ServerCom.httpRequest(urlString:url,callback: {(result:[String:Any], error: NSError?) -> () in
        // Callback aqui
    })
    ```
    
    
