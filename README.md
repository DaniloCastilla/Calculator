# Calculator
Basic and Function Calculator
package Calculadora; //Nombre del paquete donde entran las opeaciones
/**
 * @author Danilo Castilla
 * @version 1.0
 * @date 12/Sept/2017
 */
public class Base_Oper { //Inicio de la clase donde se obtendran las operaciones

	public static double suma(double a , double b){ //Se entran dos parametros en este metodo
		double c = a + b;
		return c; 

	} //Fin de metodo suma
	
    public static double resta(double a , double b){
		
		double c = a - b;
		return c;
		
	}//Fin de metodo resta

    public static int mod(int a , int b){
	
	int c = a%b;
	return c;
	
}//Fin de metodo modulo
    public static double multiplicacion(double a , double b){
		
		double c = 0;
		
		for (int i = 0 ; i<b ; i++)
		{
			
		c = suma(c , a);
			
		}//Fin del ciclo suma abreviada
		
		return c;
		
	}//Fin de metodo Multiplicacion
    
     public static double division (int a, int b){ //Entra dos valores enteros
		
		if(b != 0)
		{
			
			double c = a/b;
			
			return c;
			
		}else
		{
			
			return Double.NaN; //Si el divisor en 0, retorna como resultado NaN
			
		}
		
	}//Fin de metodo division

     public static int factorial (double d){ //Entra un solo valor
	if(d < 1)
	{
		
		return 1; //Si el numero es menor a 1, se retornara un 1
		
	}else
	{
		
		return (int) (d * (factorial(d-1))); //Se hará la operacion correspondiente de multiplicar los numeros anteriores
		
	}
}//Fin de metodo factorial
    public static double potencia (double x, double d){ //Entra dos valores como parametros, base y potencia
	
	if(d == 1)
	{
	
		return x; //Si la potencia es igual a 1, se retorna la misma base
		
	}else{
		
		if(d == 0)
		{
			
			return 1; //Si la potencia es igual a 0, se retorna siempre un 1
			
		}else{
			
			if(d > 1)
			{
				
				return (x*potencia(x, d-1));
			
			} else{
				
				return 1/potencia (x, d*(-1));
				
			}
			
		}
		
	}
}//Fin de metodo Potencia
    
    public static double Signo(double n){//Entra un numero para cambiarle el signo
    	
    	if(n % 2 == 0)
    	{
    		return 1;
    	}else{
    		return -1;
    	}
    	
    }//Fin de metodo Signo

    
    public static double ConvertGradosRadians (double x){ //Entra solo el valor que desea convertir
    	
    	return ((x*3.14159265)/180);
    	
    }//Fin de metodo Convertir grados a radianes

    public static double[] Cuadratica (int a, int b, int c){ //Entra 3 valores como parametros
    	
    	double [] x = new double [2]; //Crear un arreglo de 2 posiciones donde se almacenan los resultados
    	double discriminante; //Definir variable
    	discriminante = ((b*b)-(((4*a)*c))); //Asignar el valor
    	
    	
    	
    			if(discriminante>=0&&a!=0){
    				
    				x[0] = ((-b)+ Math.sqrt(discriminante))/(2*a);
    				x[1] = ((-b)- Math.sqrt(discriminante))/(2*a);
    				
    			}//Fin if para realizar la operacion cuadratica y asignar los valores en un arreglo
    			else{
    				
    				System.out.println("No tiene solucion en los reales ");
    			}//Fin del else para decir que una operacion cuadratica no tiene solucion en los reales
    			
    	return x;
    	
    }//Fin de metodo Operacion Cuadratica
    
     public static double Sin (double x){ //Entra solo un numero decimal o entero como parametro
		//Definir y asignar variables
		double t = 10;
		double R1 = 0;
		double x1 = Base_Oper.ConvertGradosRadians(x); //Se llama un metodo de la misma clase
		
        for(int n=0;n<t;n++){
			
R1 += (Base_Oper.Signo(n)/Base_Oper.factorial(2*n+1))*Base_Oper.potencia(x1,2*n+1);
        }//Fin ciclo para calcular Seno
        
        return R1;
	}//Fin de metodo Seno (Sin)
     
     public static double Cos (double x){ //Entra solo un numero decimal o entero como parametro
    	//Definir y asignar variables
     	double t = 10;
  		double R1 = 0;
  		double x1 = Base_Oper.ConvertGradosRadians(x); //Se llama un metodo de la misma clase
  		
          for(int n=0;n<t;n++){
  			
  			R1 += (Base_Oper.Signo(n)/Base_Oper.factorial(2*n))*Base_Oper.potencia(x1,2*n);
  		
          }//Fin ciclo para calcular Coseno
          
          return R1;
 		
 	}//Fin de metodo Coseno (Cos)
     
     
    public static double Integral(int inicio , int fin, int paso){ //Entran 3 valores enteros como parametros
    	//Definir y asignar variables
    	 double ac = 0;
    	 
    	 for(double i = inicio; i<fin; i+=paso){ 
    		 
    		 ac+=((paso)*Base_Oper.potencia(i, 2)); //Se llama un metodo de la misma clase
    		 
    	 }//Fin ciclo para calcular la Integral
    	 
    	 return ac;
    	 
     }//Fin de metodo Integral
}//Fin de la clase calculadora

//Aqui comienza una nueva clase en el mismo paquete donde entra la calculadora

package Calculadora; //Nombre del paquete donde entran las opeaciones
import java.io.*; //Paquete para las Clases Buffered

/**
 * @author Danilo Castilla
 * @version 1.0
 * @date 12/Sept/2017
 */

public class Calc_Datos {
	
	static BufferedReader br = new BufferedReader (new InputStreamReader(System.in)); // se crea la clases lectura
	static BufferedWriter bw = new BufferedWriter (new OutputStreamWriter(System.out)); // se crea la clases Escritura
	
	
	public static void main (String[]args) throws IOException{ //El Main donde se repetira todo el menú hasta que usuario decida salir
		
		int option;
		do{
			
			option = getOption();
			int [] parameters = getParameters(option);
			makeOperation(option, parameters);
			
		}while(option!=12);
		
		bw.write(getOption());
		bw.flush();
		
		
	}
	
		public static int getOption() throws IOException //Base del menú para darle la eleccion al usuario
		{
			bw.write("\n\nSeleccione por favor una de las Siguientes opciones: \n"
					+ "1. Suma\n2. Resta\n3. Multiplicacion\n4. Division\n5. Modulo \n"
					+ "6. Potencia\n7. Factorial\n8. Seno\n9. Coseno\n10.Integral\n"
					+ "11.Cuadratica\n12.Salir");
			
			bw.flush();
			
			int option = Integer.parseInt(br.readLine()); //Leer la opcion con la clase BufferedReader
		
			return option;
			
		}
		
		public static int[] getParameters(int option) throws IOException //Segun el parametro que eliga, entrara en un switch case
		{
			//Declaracion de una variable con arreglos para almacenar los numeros escritos
			int[] parameters = null;
			
			switch(option){
			
			case 1: //Suma
			{
				parameters = new int[2];
				
				bw.write("\nA continuacion se va a realizar una operacion de Suma\n");
				bw.write("Ingrese el primer numero: ");
				bw.flush();
				
				parameters[0] = Integer.parseInt(br.readLine());
				
				bw.write("Ingrese el segundo numero: ");
				bw.flush();
				
				parameters[1] = Integer.parseInt(br.readLine());
				
			}
			break;
			case 2: //Resta
			{
                parameters = new int[2];
				
				bw.write("\nA continuacion se va a realizar una operacion de Resta\n");
				bw.write("Ingrese el primer numero: ");
				bw.flush();
				
				parameters[0] = Integer.parseInt(br.readLine());
				
				bw.write("Ingrese el segundo numero: ");
				bw.flush();
				
				parameters[1] = Integer.parseInt(br.readLine());
			}
			break;
			case 3: //Multiplicacion
			{
               parameters = new int[2];
				
				bw.write("\nA continuacion se va a realizar una operacion de Multiplicacion\n");
				bw.write("Ingrese el primer numero: ");
				bw.flush();
				
				parameters[0] = Integer.parseInt(br.readLine());
				
				bw.write("Ingrese el segundo numero: ");
				bw.flush();
				
				parameters[1] = Integer.parseInt(br.readLine());
			}
			break;
			case 4: //Division
			{
                parameters = new int[2];
				
				bw.write("\nA continuacion se va a realizar una operacion de Division\n");
				bw.write("Ingrese el primer numero: ");
				bw.flush();
				
				parameters[0] = Integer.parseInt(br.readLine());
				
				bw.write("Ingrese el segundo numero: ");
				bw.flush();
				
				parameters[1] = Integer.parseInt(br.readLine());
			}
			break;
			case 5: //Modulo
			{
				parameters = new int[2];
                
				bw.write("\nA continuacion se va a realizar una operacion de Modulo\n");
				bw.write("Ingrese el primer numero: ");
				bw.flush();
				
				parameters[0] = Integer.parseInt(br.readLine());
				
				bw.write("Ingrese el segundo numero: ");
				bw.flush();
				
				parameters[1] = Integer.parseInt(br.readLine());
				
			}
			break;
			case 6: //Potencia
			{
                parameters = new int[2];
				
				bw.write("\nA continuacion se va a realizar una operacion de Potencia\n");
				bw.write("Ingrese numero de la base: ");
				bw.flush();
				
				parameters[0] = Integer.parseInt(br.readLine());
				
				bw.write("Ingrese numero de la potencia : ");
				bw.flush();
				parameters [1] = Integer.parseInt(br.readLine());
				
			}
			break;
			case 7: //Factorial
			{
				parameters = new int[1];
				 
				bw.write("\nA continuacion se va a realizar una operacion de Factorial\n");
				bw.write("Ingrese un numero: ");
				bw.flush();
				
				parameters[0] = Integer.parseInt(br.readLine());
				
			}
			break;
			case 8: //Seno
			{
				parameters = new int[1];
				
				bw.write("\nA continuacion se va a realizar una operacion de Seno\n");
				bw.write("Ingrese el numero: ");
				bw.flush();
				
				parameters[0] = Integer.parseInt(br.readLine());
				
			}
			break;
			case 9: //Coseno
			{
				parameters = new int[1];
				
				bw.write("\nA continuacion se va a realizar una operacion de Coseno\n");
				bw.write("Ingrese el numero: ");
				bw.flush();
				
				parameters[0] = Integer.parseInt(br.readLine());
				
			}
			break;
			case 10: //Integral
			{
				parameters = new int[3];
				
				bw.write("\nA continuacion se va a realizar una operacion de la Integral\n");
				bw.write("Ingrese un numero de inicio: ");
				bw.flush();
				
				parameters[0] = Integer.parseInt(br.readLine());
				
				bw.write("\nA continuacion se va a realizar una operacion de la Integral\n");
				bw.write("Ingrese un numero de fin: ");
				bw.flush();
				
				parameters[1] = Integer.parseInt(br.readLine());
				
				bw.write("\nA continuacion se va a realizar una operacion de la Integral\n");
				bw.write("Ingrese un numero de paso: ");
				bw.flush();
				
				parameters[2] = Integer.parseInt(br.readLine());
			}
			break;
			case 11: //Cuadratica
			{
				parameters = new int[3];
				
				bw.write("\nA continuacion se va a realizar una operacion de la Cuadratica\n");
				bw.write("Ingrese la Variable A: ");
				bw.flush();
				parameters[0] = Integer.parseInt(br.readLine());
				
				bw.write("Ingrese la Variable B: ");
				bw.flush();
				parameters[1] = Integer.parseInt(br.readLine());
				
				bw.write("Ingrese la Variable C: ");
				bw.flush();
				parameters[2] = Integer.parseInt(br.readLine());
			}
			break;
			
			default:
				
			{
				System.exit(0);
			}
		}
			
		return parameters; //Retornar los datos escritos por el usuario
		
		}	
		
		public static int makeOperation(int option, int[] parameters) throws IOException{ //En esta metodo, se entran a realizar las operaciones
			
			Base_Oper Oper = new Base_Oper(); //Se crea un objeto instancial a la clase Operaciones donde se sacan los metodos
			
            switch(option){
			
			case 1: //Sum
			{
				
				double result = Oper.suma(parameters[0], parameters[1]); //Llamar el metodo que sea necesario con sus parametros
				bw.write("El resultado de la suma es: " + result);
				bw.flush();
				
			}
			break;
			case 2: //Rest
			{
				
				double result = Oper.resta(parameters[0], parameters[1]); //Llamar el metodo que sea necesario con sus parametros
				bw.write("El resultado de la resta es: " + result);
				bw.flush();
						
			}
			break;
			case 3: //Multiplication
			{
               
				double result = Oper.multiplicacion(parameters[0], parameters[1]); //Llamar el metodo que sea necesario con sus parametros
				bw.write("El resultado de la multiplicacion es: " + result);
				bw.flush();
				
			}
			break;
			case 4: //Division
			{
                
				double result = Oper.division(parameters[0], parameters[1]); //Llamar el metodo que sea necesario con sus parametros
				bw.write("El resultado de la division es: " + result);
				bw.flush();
				
			}
			break;
			case 5: //Modulo
			{
				
				double result = Oper.mod(parameters[0], parameters[1]); //Llamar el metodo que sea necesario con sus parametros
				bw.write("El resultado del mudulo es: " + result);
				bw.flush();
				
			}
			break;
			case 6: //Patencia
			{
                
				double result = Oper.potencia(parameters[0], parameters[1]); //Llamar el metodo que sea necesario con sus parametros
				bw.write("El resultado de la potencia es: " + result);
				bw.flush();
				
			}
			break;
			case 7: //Factorial
			{
				
				double result = Oper.factorial(parameters[0]); //Llamar el metodo que sea necesario con sus parametros
				bw.write("El resultado del Factorial es: " + result);
				bw.flush();
				
			}
			break;
			case 8: //Seno
			{
				double result = Oper.Sin(parameters[0]); //Llamar el metodo que sea necesario con sus parametros
				bw.write("El Seno es : " + result);
				bw.flush();
			}
			break;
			case 9: //Coseno
			{
				
				double result = Oper.Cos(parameters[0]); //Llamar el metodo que sea necesario con sus parametros
				bw.write("El Coseno es : " + result);
				bw.flush();
				
			}
			break;
			case 10: //Integral
			{
				
				double result = Oper.Integral(parameters[0], parameters[1], parameters[2]); //Llamar el metodo que sea necesario con sus parametros
				bw.write("La Integral de la Funcion es : " + result);
				bw.flush();
				
			}
			break;
			case 11: //Quadratic
			{
				
				double[] x = Base_Oper.Cuadratica(parameters[0], parameters[1], parameters[2]); //Llamar el metodo que sea necesario con sus parametros
				bw.write("El resultado x1 es : " + x[0] + " \n " + "El resultado de x2 es :" + x[1]);
				bw.flush();
				
			}
			
            }
            
            return option; //Retornar el resultado
            
		}	
}
