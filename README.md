                        Proyecto: API-Decision_Helper

# Team Members
    
    Carlos Jordan
    Roberto Garcia

# Tree Structure

![](https://imgur.com/HP7xHOr)

#  Objetivos y desarrollo de la API  

    La API nace bajo el concepto de dotar de servidor y base de datos al Front-End (Decision Maker) realizado en el segundo módulo (Angular) del curso Mean-Stack. La función de la APP es resolver, de una manera objetiva y matemática, las preguntas que los usuarios puedan realizar. La función de la API es la recogida de esos datos, el CRUD de los mismos y su almacenaje en la BD. 

    ![](https://imgur.com/JvGdhPD)

        .Usuarios registrados

        ![](https://imgur.com/HIotKi3)

        .Preguntas realizadas por los usuarios registrados (notese los _id; pregunta y usuario que realizó la pregunta)

        ![](https://imgur.com/qECImJE)

        .Aspectos positivos de cada pregunta realizada.

        ![](https://imgur.com/CAwUswE)

        .Aspectos negativos de cada pregunta realizada.

        ![](https://imgur.com/R2EGdGf)


                         UTILIZACIÓN        

# URL'S

  Url del servidor, creada en el documento server.mjs (método https) pero con el puerto definido en el doc .env

  ![](https://imgur.com/k09qqtR)

  Url's (local o modo producción) de la base de datos, alojada en el documento .env

  ![](https://imgur.com/0Mtrk03)

# Formatos de respuesta

    Servidor

        ![](https://imgur.com/2AH61RE)

    Base de Datos

        Error register (https://localhost:3000/users/register)

        ![](https://imgur.com/VoxjoFF)

        Success register (https://localhost:3000/users/register)

        ![](https://imgur.com/Vbovdsg)

    

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

         ![](https://imgur.com/EaY5HWl)   

       REGISTRO CORRECTO

        ![](https://imgur.com/jAvBWmj)  

        * Opciones del new Schema (email:{lowercase: true} y this.name.toUppercase) funcionan correctamente.

        ![](https://imgur.com/lelIsMI)
         
       ERRORES

    Usuario ya existente  

        ![](https://imgur.com/m62VGtL)   

    Campo no rellenado

        ![](https://imgur.com/4vHgJBM)    



      Comprobación en la BBDD

            Antes del registro

            ![](https://imgur.com/c8DE4Za)

            Registro positivo

            ![](https://imgur.com/qhz3VFr)
    
    Respuesta caso usuario no existe en la base de datos

            ![](https://imgur.com/TDsGp4r)
            
            ![](https://imgur.com/5uUKixD)

# Token

    El token se crea en cuanto un usuario ya registrado se logea. 
    
            ./middleware/jwt_auth.mjs

            ![](https://imgur.com/sejxwGS)

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

            ![](https://imgur.com/CX4Vc5h)         

    User login correcto y creación del token.

            ![](https://imgur.com/0uUe1xh)  

    User login incorrecto

            ![](https://imgur.com/UbVjRcF)

    User login no existe

            ![](https://imgur.com/cSiaU6Y)        

    ENTRADA A LA BASE DE DATOS

        Una vez se valida el token (comparación y tiempo de expiración), se comprueban los parametros del login ( email y password), el usuario puede acceder a la base de datos y consultar, en el caso de haber utilizado la APP anteriormente, las preguntas que realizó anteriormente en la base de datos

            ![](https://imgur.com/6sDqQeM)

        O pudiendo escoger sólo la pregunta que le interese a traves del id de la misma

            ![](https://imgur.com/0SM2WO7)    


   
             
                          

            


    



