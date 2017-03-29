## Modulos iOS

**Autor**: Eduardo Leite

**Contato**: eduardo.leite@citi.ufpe.br

**Git**: eduardolsneto2

1. Get e Post Request:

    __GET__: Usando Closures (Recomendado)

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
    // faça o que quizer com o retorn da request (result)
    })
    ```
    
    __POST__ (by [rvlb-19](https://github.com/rvlb-19)):
    
    ```swift
    // Create an array of URLQueryItem that represent the key-value pairs of
    // the query.
    var queryItems = [URLQueryItem]()
    queryItems.append(URLQueryItem(name: "key", value: "value"))

    // Build the query with the data previously set
    var query = NSURLComponents()
    query.queryItems = queryItems

    // Create an URLRequest using a previously defined url and set its method
    // as POST
    var request = URLRequest(url: url)
    request.method = "POST"
    // Set the request body as the data set in query
    request.httpBody = query.query!.data(using: .utf8)

    // Send request (you can also put this inside a var if you wish)
    URLSession.shared.dataTask(with: request) { (data, response, error) in
        // Do stuff the same way as in GET
    }.resume()
    ```
