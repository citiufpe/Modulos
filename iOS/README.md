## Modulos iOS

**Autor**: Eduardo Leite

**Contato**: eduardo.leite@citi.ufpe.br

**Git**: eduardolsneto2

  1. Get e Post Request:
  
      ```GET
      
      func httpRequest(urlString:String, callback:@escaping (_ result: [String:Any], _ error: NSError?)->()){
        var dic = [String:Any]()
        let url = NSURL(string: urlString)
        let task = URLSession.shared.dataTask(with: url! as URL) {(data, response, error) in
            
            do {
                if let data = data,
                    let json = try JSONSerialization.jsonObject(with: data) as? [String: Any]{
                    dic = json
                    print(json)
                    callback(dic,error as NSError?)
                }
            } catch {
                print("Error deserializing JSON: \(error)")
            }
        }// finishing the http request
        task.resume()
    }
    ```
    
