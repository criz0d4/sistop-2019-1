PROBLEMA: Santa CLaus
Fuente: Little book of semaphores (Allen B. Downey) (p. 149)

Planteamiento
-Santa Claus duerme en el Polo Norte mientras sus elfos
trabajan fren�ticamente en la construcci�n de millones de
nuevos juguetes.
-A veces se topan con un problema. Pueden pedir ayuda a
Santa Claus, pero s�lo de tres en tres.
-Sus nueve renos pasan todo el a�o de vacaciones en las playas
del Caribe.
-Santa debe despertar a tiempo para iniciar su viaje anual.

Reglas
-Si los nueve renos est�n de vuelta, es hora de despertar a
Santa Claus para que inicie su recorrido.
-Si los elfos tienen problemas construyendo alg�n juguete, le
piden ayuda a Santa Claus.
Pero para no darle demasiada lata, lo hacen s�lo cuando hay
tres elfos que tienen un problema. Mientras tanto, lo dejan
dormir.
-Puede haber cualquier cantidad de elfos.
_______________________________________________________________

La soluci�n al problema planteado la implement� en Python
Versi�n del compilador de linux: 2.7.6
_______________________________________________________________

ESTRATEGIA SEGUIDA

Para esta soluci�n, tom� en cuenta que tanto los duendes (elfos)
as� como los renos, solicitaban la atenci�n de Santa Claus.
Por ello, defin� a Santa Claus como un recurso, limitando su uso
mediante un sem�foro, el cu�l se vuelve cero cuando atiende al 
grupo de 3 duendes o de 9 renos.
Existe un contador para saber el n�mero de renos que han vuelto,
y un contador para saber cuando 3 duendes est�n esperando ayuda.
Las modificaciones de cada contador est�n protegidas mediante un
�nico mutex.
Finalmente utilic� otro sem�foro a manera de torniquete (que en
este caso su funci�n es m�s similar al de un cadenero). Una vez
que 3 duendes acceden al �rea de espera, el torniquete se bloquea
hasta que los anteriores salgan. De igual forma, los renos llegan
uno a uno sin necesidad de formarse, hasta que se reunen los 9 y 
solo en ese momento bloquean el torniquete hasta que se adue�an
de Santa.
________________________________________________________________

COMENTARIOS

1. Despu�s de n errores y n correcciones, conoc� de cara a los
bloqueos mutuos y a las inaniciones, ya que cuando se implementa
mal el orden de adquisici�n y liberaci�n de Santa, el Torniquete
y/o el Mutex, un hilo puede estar esperando un recurso A para
liberar el recurso B que posee, mientras que otro hilo esta a la 
espera del recurso B para liberar al A. Luego entonces el proceso
se queda en el limbo eternamente.

2. En la soluci�n actual, cuando se junta el grupo de 3 duendes,
el contador simplemente regresa a 0 para dar espacio a que otro
grupo de 3 duendes esperen por Santa Claus, simulado haber sido
atendidos. Posteriormente se podr�a implementar una funci�n 
secuencial o por lote (de 3) con la que los duendes interactuen
con Santa Claus antes de volver a sus trabajos.

3. En alg�n punto entran m�s de 3 duendes al �rea de espera.

