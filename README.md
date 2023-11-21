# The filter-suggester Microservice
This github repo contains the implementation for the filter-suggester microservice. This readme contains the
communication contract that demonstrates how to use the microservice

# Communication Contract

## A - How to REQUEST data from the microservice

1. Ensure that the microservice is running. Follow these steps to get started:
    - `git clone` this repository
    - create and active a virtual environment
      `python3 -m venv venv`\
      `source venv/bin/activate`
    - Install required dependencies\
      `pip install -r requirements.txt`
    - run the microservice\
    `python3 filter-suggester.py`
    - The microservice will print `The filter-suggestor microservice is online` when operational
      
2. `import zmq` and `import json` into the project from which you wish to call the microservice
3. The following code shows an example call to the microservice to request (and receive) data
    ```
    import zmq
    import json
    
    context = zmq.Context()
    socket = context.socket(zmq.REQ)
    socket.connect("tcp://localhost:5555")
    socket.send(b"search filter")   # sending the request!
    
    json_data = socket.recv_string() # receiving the request!
    filters_dict = json.loads(json_data) # converting json into a Python dictionary
    ```
    Example return
    ```
   {'distance': 146, 'city': 'Chicago', 'zipcode': '60601', 'min-price': 5422, 'max-price': 28262, 'make': 'BMW', 
   'model': '5 Series', 'min-odometer': 99555, 'max-odometer': 157649, 'min-year': 1955, 'max-year': 2012, 
   'transmission': 'automatic', 'drive': 'fwd', 'condition': 'fair', 'color': 'brown', 'title': 'parts only'}

    ```

## B - How to RECEIVE data from the microservice
1. Make sure the microservice is running -- this means that the microservice is ready to accept requests and send back responses
2. Call the microservice using a call such as the one demonstrated above to request data from the microservice
3. Use `socket.recv_string()` to actually receive the data from the microservice's response
4. The example call above demonstrates how to use `socket.recv_string()` to RECEIVE data from the microservice. 
   The example above shows both how to REQUEST and RECEIVE data from the microservice.


## C - UML Diagram
![microservice UML (1)](https://github.com/neilnautiyal/cs361-microservice/assets/75712709/9f74bd41-0163-445c-8410-b85d898c298e)
