                        Proyecto: API-Decision_Helper

# Team Members
    
. Carlos Jordan  
. Roberto Garcia

# Tree Structure

![](https://imgur.com/FUbrrbI.png)

#  Objetivos y desarrollo de la API  

La API nace bajo el concepto de dotar de servidor y base de datos al Front-End (Decision Maker) realizado en el segundo módulo (Angular) del curso Mean-Stack.

. La función de la APP es resolver, de una manera objetiva y matemática, las preguntas que los usuarios puedan realizar. 

. La función de la API es la recogida de esos datos, el CRUD de los mismos y su almacenaje en la BD. 



UTILIZACIÓN        

# URL'S

Url del servidor. Se crea en el documento server.mjs (método *https para localhost) pero con el puerto definido en el doc .env
  
 *Debemos recordar que al subir al nuestra aplicación al servidor HEROKU, el mismo nos crea el https, con lo cual debemos modificar en nuestro documento server.js 

            https.createServer(opt, app).listen(process.env.PORT)
por

            http.createServer(app).listen(process.env.PORT)

En el documento  .env es donde definiremos las rutas de:

        . Puerto servidor
                    . localhost
                    . Heroku (modo producción)

        . Base de datos
                    . localhost://27017
                    . mongo Atlass

![](https://imgur.com/0Mtrk03.png)

# Creación del token

Objeto creación token ./api/middleware/jwt_auth.js

En el documento jwt_auth definimos la manera en que el token será creado:

. Duración del token
. Fecha finalización token
. Codificación token

                        export default {
                            createToken(user) {
                              const f1 = moment().unix();
                              const f2 = moment().add(14, "days");
                              const payload = {
                                sub: user,
                                iat: f1,
                                exp: f2.unix()
                              };
                              const salidaToken = {
                                orig: payload,
                                fech: f2,
                                token: jwt.encode(payload, process.env.SECRET_TOKEN)
                              };
                              return salidaToken;
                            },
                        
Pasos para obtener un token válido:

. SignUp (https://api-decision-helper.herokuapp.com/users/register)

![](https://imgur.com/Vbovdsg.png)

. SignIn  (https://api-decision-helper.herokuapp.com/users/oginl)

![](https://imgur.com/0uUe1xh.png)

Enlace postman

(https://documenter.getpostman.com/view/9175109/SW18waDu)



# Formatos de respuesta



Servidor

En la creación del servidor hemos dejado el único console.log de todo el documento, informando de la conexión del servidor al puerto (local o Heroku) seleccionado.

![](https://imgur.com/2AH61RE.png)

Base de Datos

Error register (https://localhost:3000/users/register)

![](https://imgur.com/VoxjoFF.png)

Success register (https://localhost:3000/users/register)

![](https://imgur.com/Vbovdsg.png)

    

        Creación Usuario

        <nombre src:[API-Decision-Helper]>/middleware/create.mjs

En la creación de los usuarios tenemos varios pasos. Primero hemos creado un new Schema de usuario en nuestro documento ./models/schema.mjs y luego un método para guardar el nuevo usuario registrado si no existe previamente.

Hemos definido en nuestro schema:
            . Tipo de mensaje: String
            . Sin espacios en blanco (los elimina el objeto directamente)
            . Mail sin espacios en blanco ni antes ni después del @ y ningumo después del punto
            . Todos los campos son obligatorios, no pueden quedar en blanco
            . Nombre en mayúscula
            . Encriptación del password

![](https://imgur.com/EaY5HWl.png)   

       REGISTRO CORRECTO

![](https://imgur.com/jAvBWmj.png)  

        * Opciones del new Schema (email:{lowercase: true} y this.name.toUppercase) funcionan correctamente.

![](https://imgur.com/lelIsMI.png)
         
       ERRORES

    Usuario ya existente  

![](https://imgur.com/m62VGtL.png)   

    Campo no rellenado

![](https://imgur.com/4vHgJBM.png)    



      Comprobación en la BBDD

            Antes del registro

![](https://imgur.com/c8DE4Za.png)

            Registro positivo

![](https://imgur.com/qhz3VFr.png)
    
    Respuesta caso usuario no existe en la base de datos

![](https://imgur.com/TDsGp4r.png)
            
![](https://imgur.com/5uUKixD.png)

# Token

    El token se crea en cuanto un usuario ya registrado se logea. 
    
            ./middleware/jwt_auth.mjs

![](https://imgur.com/sejxwGS.png)

            La duración de los tokens se puede modificar en:

                    const payload = {
                                sub: user,
                                iat: moment().unix(),
                                exp: moment()                                
                               ==>  .add(14, "days") ==> Entre los paréntesis duración del token:  
                                  .unix()  <==            "seconds", "minutes", "hours","days", "months", "years"
                              };

            * Documentación relativa a moment.js
(https://momentjs.com/docs/)
(https://flaviocopes.com/momentjs/)

    En el momento de la creación  del token, también se codifica el mismo con la configuración de SECRET_TOKEN, adjunta el el documento .env

![](https://imgur.com/CX4Vc5h.png)         

    User login correcto y creación del token.

![](https://imgur.com/0uUe1xh.png)  

    User login incorrecto

![](https://imgur.com/UbVjRcF.png)

    User login no existe

![](https://imgur.com/cSiaU6Y.png)        

    ENTRADA A LA BASE DE DATOS

        Una vez se valida el token (comparación y tiempo de expiración), se comprueban los parametros del login ( email y password), el usuario puede acceder a la base de datos y consultar, en el caso de haber utilizado la APP anteriormente, las preguntas que realizó anteriormente en la base de datos

![](https://imgur.com/6sDqQeM.png)

        O pudiendo escoger sólo la pregunta que le interese a traves del id de la misma

![](https://imgur.com/0SM2WO7.png)    


   
(https://web.postman.co/collections/9175109-8f2ce70b-c8aa-4a28-9090-4ffee58f18c9?version=latest&workspace=ed7b3597-9f25-482f-b6a4-094d3f7d65af)            
                          

            


    



