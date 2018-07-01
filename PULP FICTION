%pareja(Persona, Persona)
pareja(marsellus, mia).
pareja(pumkin,    honeyBunny).

%trabajaPara(Empleador, Empleado)
trabajaPara(marsellus, vincent).
trabajaPara(marsellus, jules).
trabajaPara(marsellus, winston).

%1
saleCon(Quien,Cual):-
	pareja(Quien,Cual).
saleCon(Quien,Cual):-
	saleCon(Cual,Quien).


/*Caso Base: 	saleCon(Quien,Cual):-
			pareja(Quien,Cual).	

Caso Recursivo:	saleCon(Quien,Cual):-
				saleCon(Cual,Quien). */

%2
pareja(bernardo, bianca).
    pareja(bernardo, charo).

%3
trabajaPara(Empleador,bernardo):-
	trabajaPara(marsellus,Empleador),
	Empleador\=jules.
trabajaPara(Empleador, george):-
	saleCon(Empleador,bernardo).

%4
esFiel(Persona):-
	not((saleCon(Persona,Amante1),
	saleCon(Persona,Amante2),
	Amante1\=Amante2)).
  
%5
acataOrden(Persona1, Persona2):-
	trabajaPara(Persona1,Persona2).
	    
	   acataOrden(Persona1, Persona2):-
	trabajaPara(Persona1,Jefe),
	acataOrden(Jefe, Persona2).
  
  % personaje(Nombre, Ocupacion)
personaje(pumkin,     ladron([estacionesDeServicio, licorerias])).
personaje(honeyBunny, ladron([licorerias, estacionesDeServicio])).
personaje(vincent,    mafioso(maton)).
personaje(jules,      mafioso(maton)).
personaje(marsellus,  mafioso(capo)).
personaje(winston,    mafioso(resuelveProblemas)).
personaje(mia,        actriz([foxForceFive])).
personaje(butch,      boxeador).
personaje(bernardo,   mafioso(cerebro)).
personaje(bianca,     actriz([elPadrino1])).
personaje(elVendedor, vender([humo, iphone])).
personaje(jimmie,     vender([auto])).

% encargo(Solicitante, Encargado, Tarea). 
% las tareas pueden ser cuidar(Protegido), ayudar(Ayudado), buscar(Buscado, Lugar).

encargo(marsellus, vincent,   cuidar(mia)).
encargo(vincent,  elVendedor, cuidar(mia)).
encargo(marsellus, winston, ayudar(jules)).
encargo(marsellus, winston, ayudar(vincent)).
encargo(marsellus, vincent, buscar(butch, losAngeles)).
encargo(bernardo, vincent, buscar(jules, fuerteApache)).
encargo(bernardo, winston, buscar(jules, sanMartin)).
encargo(bernardo, winston, buscar(jules, lugano)).

amigo(vincent, jules).
amigo(jules, jimmie).
amigo(vincent, elVendedor).

%1
esPeligroso(Personaje):-
		personaje(Personaje,mafioso(maton)).

	esPeligroso(Personaje):-
		personaje(Personaje,ladron(Objetivos)),
		member(licorerias,Objetivos).

	esPeligroso(Personaje):-
		trabajaPara(Jefe,Personaje),
		esPeligroso(Jefe).

%2
 sanCayetano(Persona):-
	tieneCerca(Persona,_),
  forall(tieneCerca(Persona,Alguien), encargo(Persona,Alguien,_)).

tieneCerca(Alguien,Persona):-
	amigos(Persona,Alguien).

tieneCerca(Persona,Alguien):-
	trabajaPara(Persona,Alguien).

tieneCerca(Persona,Alguien):-
	trabajaPara(Alguien,Persona).

%3
nivelRespeto(vincent,15).
  
nivelRespeto(Persona,Nivel):-
	personaje(Persona,Ocupacion),
	asignarNivel(Ocupacion,Nivel),
	Persona\=vincent.

asignarNivel(actriz(Peliculas),Nivel):-
	length(Peliculas,Longitud),
	Nivel is Longitud/ 10.

asignarNivel(mafioso(resuelveProblemas),10).

asignarNivel(mafioso(capo),20).

asignarNivel(Ocupacion,0):-
	Ocupacion\=actriz(_),
	Ocupacion\=mafioso(resuelveProblemas),
	Ocupacion\=mafioso(capo).
	
%4
esPersonajeRespetable(Persona):-
	nivelRespeto(Persona, Nivel),
	Nivel>9.
noEsPersonajeRespetable(Persona):-
  nivelRespeto(Persona, Nivel),
	Nivel=<9.

respetabilidad(Respetables,NoRespetables):-
  findall(Personaje,esPersonajeRespetable(Personaje),ListaRespetables),
  length(ListaRespetables,Respetables),
  findall(Personaje,noEsPersonajeRespetable(Personaje),ListaNoRespetables),
  length(ListaNoRespetables,NoRespetables).

%5
masAtareado(Personaje):-
	personaje(Personaje,_),
	forall(personaje(Persona,_),esElMasAtareado(Personaje,Persona)).

esElMasAtareado(Personaje,Persona):-
	cantidadEncargos(Personaje,Cantidad),
	cantidadEncargos(Persona,Cantidad2),
	Cantidad>=Cantidad2.

cantidadEncargos(Personaje,Cantidad):-
  findall(Encargo,encargo(_,Personaje,_),Encargos),
  length(Encargos,Cantidad).	


