/*                Automatismo toldo

Práctica na que simulamos o funcionamento dun toldo, que se vai a estirar ou non en función do nivel de brillo que reciba un pin LDR.
Este pin é unha resistencia variable na que cando non percibe luz a súa resistencia é alta e cando percibe luz a resistencia disminúe ata ser casi 0.
A partir de aquí asignamos unha variable (umbral) na que asignamos un valor, co que queremos conseguir que cando a lectura da LDR o seu valor sexa maior
ca o do umbral se active un relé que vai facer funcionar un motor que sería o que estira o toldo. Para que o motor traballe un tempo determinado,
asignámolle un contador que vai restando unha unidade segundo se executa o programa en bucle. Cando o contador chega a 0,o motor para.





Entradas: pin analóxico A0
Saídas: pin dixital 12

Autor: Manuel Dominguez
data: 3 Marzo



*/
#define RELE 12				
#define LDR A0


int umbral = 950;      		 // Declaramos int; o que lle comunica a Arduino que é unha variable enteira, neste caso asociado ao comando umbral
int entrada = -1;			/* Asignámolle un valor enteiro a "entrada"; neste caso -1, para que no momento da lectura se vemos que sigue marcando -1 
								non está leendo o valor da ldr correctamente */
bool releON = false;		// Declaramos releON coma unha variable Booleana, na que vamos ter 2 estados (true-false), neste caso queremos que de inicio sexa false
int contador = 100;			// utilizámolo para o tempo de funcionamento do motor

void setup(){				// Esta parte arduino só a vai leer unha vez, é donde indica os modos de traballo dos pins
  
 pinMode(RELE, OUTPUT);		// Indicamos que 	RELÉ é unha saída
 pinMode(LDR, INPUT);    	// Indicamos que LDR é unha entrada
 Serial.begin(9600);		// Dicímolle cal queremos que sexa a velocidade de comunicación
}






void loop(){					// Aquí é donde escribimos o programa e como queremos que funcione, e se repitya en bucle
  			//LECTURA ENTRADAS
  
 entrada = analogRead(LDR);   // Funcion na que lle asignamos que cando escribamos "entrada", lea o valor da LDR, definida no pin A0. O RANGO É 54 - 974
 Serial.print("Valor entrada LDR: "); 	// Aqui escribimos no monitor serie:  "valor da entrada LDR"
 Serial.println(entrada);				// Aqui queremos que imprima o valor da entrada no monitor serie
 
  
  		//ACCIONAMENTO ACTUADORES
  if(entrada > umbral)  { 	 //comprobar que si o valor da entrada do ldr sexa maior que o valor do umbral, neste caso 950 realice o seguinte
    releON = true;			// Dicimos que o relé encenda		
  	contador ;				// Queremos que se active o contador, que comeza en 100
   
  }
 
  if(entrada > umbral && contador > 0) {	/* Funcion na que dicimos que si ao valor da entrada(LDR) é maior que o umbral (950)
    										e ademáis si o contador é maior que cero, faga o seguinte*/
    
	Serial.print("Contador:  "); Serial.println(contador);  // Imprimir "Contador "
    contador --;											// O contador reste unha unidade cada vez que execute o ciclo
    delay(70);												// Esperar 70 milisegundos ata que volva leer función de novo
  }
  else  {				// Función na que nos di que se non se cumple o anterior, faga o seguinte
     releON = false;	// apagar o relé
  }
 
   digitalWrite(RELE, releON);  // dicimos no programa que (RELE, releON) é unha saída dixital
}

















