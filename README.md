Synaptic.NET

Le projet est bas� sur Moleculer

Le concept est simple: d�composer un syst�me en micro-services �crits dans des containers
sp�cialis�s plut�t que des Api Rest, Grpc ou Websocket brutes

Un micro-service impl�mente l'interface [ISynapticService]
Un micro-service est d�compos� en
- Actions (handler de requ�tes) d�signent toutes les m�thodes publiques d'un SynapticService
- les Actions peuvent �tre d�cor�es des attributs [Authorize(Roles, Policy), HttpPost, HttpGet, HttpPut, HttpPatch, HttpDelete] 
- EventHandlers / EventProcessors d�cor�es � l'aide de l'attribut [SynapticEventHandler]
- Methodes (au sens OO) qui sont les m�thodes priv�es d'un SynapticService
- Description (propri�t�)
- Name (prop)
- Version (prop)
- Dependences (sp�cifie les d�pendances sur les services) gr�ce � l'attribut [SynapticServiceDependency(Name, Version)]


Une SynapticAction est une m�thode, elle peut retourner n'importe quel objet ex: un poco, etc
une SynapticAction qui retourne void est une FiniteEvaluator. Elle noie/termine une requ�te.
retourne une NoContentResult avec le code http correspondant.

Une SynapticAction Accepte des param�tres comme toute Action d'un controlleur MVC.
- Un objet de type ISynapticContext disponible par d�faut (recommand� de l'injecter par constructeur)
- Si ajout� aux param�tres d'une action d�cor�e avec l'attribut [SynapticAction], Synaptic.NET se chargera de l'injecter

Uen SynapticEventHandler est une m�thode qui traite d'un event 
- est obligatoirement g�n�rique (T). T repr�sente le type de l'�v�nement
- retourne obligatoirement void ou Task
- Un objet de type SynapticContext disponible par d�faut (recommand� de l'injecter par constructeur)




[Version 2: Services are Stateful and State can be serialized]