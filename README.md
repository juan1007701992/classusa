class Polinomio:
    def __init__(self, coeficientes):
        self.coeficientes=coeficientes
        
    def mostrar_poli(self):
        "acumulador
        x=""
        for i in range(len(self.coeficientes)):
            if i==0:
                x += str(self.coeficientes[i])
            else:
                x=x + "+" + str(self.coeficientes[i])+"X**"+str(i)
        print (x)
    
    def grado (self):
    #Se quita el ultimo elemento ya que la constante no se toma
        return len(self.coeficientes)-1      
    
    def evaluar (self,x):
    #variable acumulativa
        resultado=0
        for i in range (len(self.coeficientes)):
            resultado=resultado + self.coeficientes[i]*x**i
        return resultado
    
    def suma_polinomio(self, otro_polinomio):
        #funcion que permitira dar el rango para dar la condicion cuando los objetos tengan distinta longitud
        k=max(len(self.coeficientes), len(otro_polinomio.coeficientes))
        #funcion que permitira dar renstriccion del primer condicional
        a=min(len(self.coeficientes), len(otro_polinomio.coeficientes))
        #contador
        b=0
        #lista que permitira añadir los valores de la suma de objetos
        list_1=[]
        #condicion
        while b!=a:
            #variable que sumara los objetos que tengan la misma longitud
            c=self.coeficientes[b]+otro_polinomio.coeficientes[b]
            b+=1
            list_1.append(c)
         
        #permitira añadir valores a objetois que tengan distinta longitud
        for  i in range(b,k):
            #condicion
            if len(self.coeficientes)>len(otro_polinomio.coeficientes):
                c=self.coeficientes[i]
                list_1.append(c)
            #condicion contraria a la inicial
            elif len(self.coeficientes)<len(otro_polinomio.coeficientes):
                c=otro_polinomio.coeficientes[i]
                list_1.append(c)
        
           #ejecucion      
        return Polinomio(list_1)
   
   def __neg__(self):
   #permite mostrar el polinomio opuesto 
        c= Polinomio([-self.coeficientes[i] for i in range (0,len(self.coeficientes))])
        return c.mostrar()
    
    def __rmul__(self,x):
    #permite multiplicar escalares con polinomios
        c= Polinomio([(x)*self.coeficientes[i] for i in range (0,len(self.coeficientes))])
        return c.mostrar()
   
    def raices(self):
        if self.grado()>2:
            print ('funcion no definida')
        elif self.grado()==2:
        #raiz con ecuacion con signo positivo
            c= -self.coeficientes[1]+((self.coeficientes[1]**2)-((4*self.coeficientes[0])*(self.coeficientes[2])))**(0.5)
            b= c/(2*self.coeficientes[0])
            print (b)
            raiz con ecuacion con signo negativo
            m=-self.coeficientes[1]-((self.coeficientes[1]**2)-((4*self.coeficientes[0])*(self.coeficientes[2])))**(0.5)
            n=m/(2*self.coeficientes[0])
            print (n)
            return
        else:
             for i in range (0,10000):
                 self.evaluar(i)
                 if self.evaluar()==0:
                     print (i)
    
class matriz:
    def __init__(self,coordenadas):
        self.coordenadas= coordenadas
        self.filas=len(coordenadas)
        self.columnas=len(coordenadas[0])
        for i in self.coordenadas:
            if self.columnas != len(i):
                print ('columnas mal establecidas')
               #si el objeto no cumple la condicion de las columnas, los metodos descritos a continucacion no se ejecutaran
                break
    
    def __add__(self, otra_matriz):
        #condicion de matrices de misma dimension 
        if self.filas== len(otra_matriz) and self.columnas==len(otra_matriz[0]):
            resul=[]
            #for que ira para cada fila establecida del objeto
            for i in range(len(self.coordenadas)):
                fila=[]
                #for que ira a cada elemento de la fila
                for x in range(len(self.coordenadas[i])):
                    #suma de cada elemento de la  fila  de una matriz a otra
                    c=self.coordenadas[i][x]+otra_matriz[i][x]
                    fila.append(c)
             
                resul.append(fila)
        print(resul)
    
    def __remul__(self,y):
        resul=[]
        #  #for que ira para cada fila establecida del objeto
        for i in range(len(self.coordenadas)):
            fila=[]
            #for que ira a cada elemento de la fila
            for x in range(len(self.coordenadas[i])):
                #multiplicacion de cada elemento de la fila por un escalar 
                c=(self.coordenadas[i][x])*y
                fila.append(c)
                     
            resul.append(fila)
        print(resul)    
        
        
import numpy as n
#Clase vector
class vector:
    def __init__(self,coordenadas):
        self.coordenadas=coordenadas
        
    def __neg__(self):
    # permite hallar el vector opuesto al evaluado
        return vector([(-1)*self.coordenadas[i] for i in range (0,len(self.coordenadas))])
         
    def __add__(self,otro_vector):
        if len(self.coordenadas) != len(otro_vector.coordenadas):
            print('vectores de distinta dimension.ERROR')
        else:
        #Realiza suma de los coeficientes por posicion 
            return vector([self.coordenadas[i] + otro_vector.coordenadas[i] for i in range (0,len(self.coordenadas))])
    
    def __sub__(self,otro_vector):
        if len(self.coordenadas) != len(otro_vector.coordenadas):
        #Realiza resta de los coeficientes por posicion 
            print('vectores de distinta dimension.ERROR')
        else:
            return vector([self.coordenadas[i] - otro_vector.coordenadas[i] for i in range (0,len(self.coordenadas))])
   
    def dot(self,otro_vector):
        if len(self.coordenadas) != len(otro_vector.coordenadas):
            print ('vectores de distinta dimension')
            return
        else:
        #acumulador
           z=0
           for i in range (0,len(self.coordenadas)):
           #realiza multiplicacion punto de vectores
               b=self.coordenadas[i]*otro_vector.coordenadas[i]
               z=b+z
        return z
        
    def longitud(self):
    #definicion de longuitud de vectores en R**2
        c=self.dot(self)
        return c**(1/2)
    
    def length(self,z):
    #definicion general de la longuitud del vector
            c=sum([self.coordenadas[i]**z for i in range (0,len(self.coordenadas))])
            print (c**(1/z))
            
    def separacion(self,otro_vector):
      #angulo que forma los 2 vectores evaluados 
        if len(self.coordenadas) != len(otro_vector.coordenadas):
            print('vectores de distinta dimension.ERROR')
            return
        else:
            return (self.dot(otro_vector))/(self.longitud()*otro_vector.longitud())
     
    def distancia(self, otro_vector):
       #distancia de 2 vectores 
       a=self - otro_vector
        return a.longitud()
    
    def normalizar(self):
        result=[]
         #funcion para normalizar un vector
        c=((self.coordenadas[i])/(self.longitud()) for i in range(0, len(self.coordenadas)))
        result.append(c)
        return vector(result)
   
    def angulo(self, otro_vector):
     #funcion que permite hallar el angulo de un vector
        return n.arccos(self.separacion(otro_vector))
 
    def polar(self):
        if len(self.coordenadas) != 2:
            print ('funcion no definida')
            return
        else:
        #funcion que permite poner un vector a su forma polar
            v=vector([1,0])
            return [self.longitud(), self.angulo(v)]
 
#funcion que permite poner de polar a vector 
def f(x,y):
       c=x*(n.cos(y))
       b=((x)**2-(c)**2)**(1/2)
       return [c,b]
   
    
class Vspace:
    def __init__(self, coeficientes):
        self.coef = coeficientes
    
    def __repr__(self):
    #mostrar el vector
        return f'VS({self.coef})'
    
    def __len__(self):
    #longitud
        return len(self.coef)
  
    def __getitem__(self, i):
      #Llamar un elemento
        return self.coef[i]
 
    def __add__(self, v2):
       #Suma tradicional
        return Vspace(list(map(lambda a,b:  a+b, self.coef, v2.coef)))
  
    def __sub__(self, v2):
      #Resta tradicional
        return Vspace(list(map(lambda a,b:  a-b, self.coef, v2.coef)))

    def __neg__(self):
    #vector opuesto
        return Vspace(list(map(lambda a:  -a, self.coef)))
   
    def __mul__(self, x):
     #Multiplicacion de vectores
        if type(x) == type(1) or type(x) == type(1.0):
            return Vspace(list(map(lambda y: x*y, self.coef)))
        elif type(self) == type(x):
            return Vspace(list(map(lambda a,b:  a*b, self.coef, x.coef)))
      
    def __rmul__(self, x):
    #multiplicacion de escalar por vector
        return self * x
   
    def __pow__(self, x):
     #Potenciacion 
        if type(x) == type(1) or type(x) == type(1.0):
            return Vspace(list(map(lambda y: y**x, self.coef)))
      
    def norm(self, p = 2):
    #Norma tradicional (Euclidiana)  
        if type(p) == type(1) or type(p) == type(1.0):
            return (sum(map(lambda x: abs(x) ** p, self.coef)))**(1/p)
        elif p == 'inf':
            return max(self.coef)
     
     
class Polynomial(Vspace):
    def __init__(self, coeficientes):
#Condicion que permite quitar los ceros que estan a la derecha de los polinomios
        while coeficientes[-1]==0:
              coeficientes.pop()
        super().__init__(coeficientes)
         
    def __repr__(self):
    #metodo que permite ver el los coeficientes del polinomio  
        return f'Polynomial({self.coef})'

    def __neg__(self):
    #metodo que permite ver el polinomio opuesto
        return Polynomial(super().__neg__().coef)
 
    def norm(self, p = 2):
    #metodo que permite ver la longitud
        return super().norm(p)
 
    def grado(self):
    #metodo que permite ver el grado 
        return len(self.coef)-1
 
    def __mul__(self, p2):
        #grado del nuevo polinomio
        d=self.grado()+p2.grado()
        result=[]
        s=0
        #variables que permitiran no realizar cambios a los polinomios
        coef_1=self.coef.copy()
        coef_2=p2.coef.copy()
        
        #permitira añadir 0 con el objetivo de volver el grado los polinomios
        for i in range (d):
            if self.grado()!=d:
                coef_1.append(0)
            if p2.grado()!=d:
                coef_2.append(0)
       #definicion de la sumatoria
        for i in range(d+1):
            for j in range(i+1):
                c=coef_1[j]*coef_2[i-j]
                s=c+s
            result.append(s)
            s=0
             
        return Polynomial(result)
     
    def __pow__(self,x):
     #funcion que  permitira hallar la exponencial del polinomio
        p=self
        #permitira definir el valor de la exponencial
        for i in range(1,x):
            p=p*self
         
        return p
