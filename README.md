class Polinomio:
    def __init__(self, coeficientes):
        self.coeficientes=coeficientes
    def mostrar_poli(self):
        x=""
        for i in range(len(self.coeficientes)):
            if i==0:
                x += str(self.coeficientes[i])
            else:
                x=x + "+" + str(self.coeficientes[i])+"X**"+str(i)
        print (x)
    def grado (self):
        return len(self.coeficientes)-1      
    def evaluar (self,x):
        resultado=0
        for i in range (len(self.coeficientes)):
            resultado=resultado + self.coeficientes[i]*x**i
        return resultado
    #funcion que permitira la suma de 2 objetos de la clase
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
        c= Polinomio([(-1)*self.coeficientes[i] for i in range (0,len(self.coeficientes))])
        return c.mostrar()
    
    def __rmul__(self,x):
        c= Polinomio([(x)*self.coeficientes[i] for i in range (0,len(self.coeficientes))])
        return c.mostrar()
    
    
    def raices(self):
        if self.grado()>2:
            print ('funcion no definida')
        elif self.grado()==2:
            c= -self.coeficientes[1]+((self.coeficientes[1]**2)-((4*self.coeficientes[0])*(self.coeficientes[2])))**(0.5)
            b= c/(2*self.coeficientes[0])
            print (b)
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
    #constructor 
    def __init__(self,coordenadas):
      #condiciones de los  elementos   
        self.coordenadas= coordenadas
        self.filas=len(coordenadas)
        self.columnas=len(coordenadas[0])
        for i in self.coordenadas:
            if self.columnas != len(i):
                print ('columnas mal establecidas')
               #si el objeto no cumple la condicion de las columnas, los metodos descritos a continucacion no se ejecutaran
                break
    #suma de matrices       
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
     
    #multiplicacion de matrices por escalar
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
        
#Biblioteca
import numpy as n
#Clase vector
class vector:
    #Constructor
    def __init__(self,coordenadas):
        self.coordenadas=coordenadas
    #Funcion que permite hallar el vector opuesto al evaluado
    def __neg__(self):
        return vector([(-1)*self.coordenadas[i] for i in range (0,len(self.coordenadas))])
    #suma de vectores        
    def __add__(self,otro_vector):
        if len(self.coordenadas) != len(otro_vector.coordenadas):
            print('vectores de distinta dimension.ERROR')
        else:
            return vector([self.coordenadas[i] + otro_vector.coordenadas[i] for i in range (0,len(self.coordenadas))])
    #Resta de vectores
    def __sub__(self,otro_vector):
        if len(self.coordenadas) != len(otro_vector.coordenadas):
            print('vectores de distinta dimension.ERROR')
        else:
            return vector([self.coordenadas[i] - otro_vector.coordenadas[i] for i in range (0,len(self.coordenadas))])
    #Producto punto    
    def dot(self,otro_vector):
        if len(self.coordenadas) != len(otro_vector.coordenadas):
            print ('vectores de distinta dimension')
            return
        else:
           z=0
           for i in range (0,len(self.coordenadas)):
               b=self.coordenadas[i]*otro_vector.coordenadas[i]
               z=b+z
        return z
    #Radio del vector                
    def longitud(self):
        c=self.dot(self)
        return c**(1/2)
    #Radio en general 
    def length(self,z):
            c=sum([self.coordenadas[i]**z for i in range (0,len(self.coordenadas))])
            print (c**(1/z))
   #Angulo que forma los 2 vectores evaluados 
    def separacion(self,otro_vector):
        if len(self.coordenadas) != len(otro_vector.coordenadas):
            print('vectores de distinta dimension.ERROR')
            return
        else:
            return (self.dot(otro_vector))/(self.longitud()*otro_vector.longitud())
     
    #Distancia de 2 vectores  
    def distancia(self, otro_vector):
        a=self - otro_vector
        return a.longitud()
    #funcion para normalizar un vector
    def normalizar(self):
        result=[]
        c=((self.coordenadas[i])/(self.longitud()) for i in range(0, len(self.coordenadas)))
        result.append(c)
        return vector(result)
    #funcion que permite hallar el angulo de un vector
    def angulo(self, otro_vector):
        return n.arccos(self.separacion(otro_vector))
 
    #funcion que permite poner un vector a su forma polar
    def polar(self):
        if len(self.coordenadas) != 2:
            print ('funcion no definida')
            return
        else:
            v=vector([1,0])
            return [self.longitud(), self.angulo(v)]
 
#funcion que permite poner de polar a vector 
def f(x,y):
       c=x*(n.cos(y))
       b=((x)**2-(c)**2)**(1/2)
       return [c,b]
   
    
class Vspace:
    #Constructor general
    def __init__(self, coeficientes):
        self.coef = coeficientes
    #Print    
    def __repr__(self):
        return f'VS({self.coef})'
    #Len
    def __len__(self):
        return len(self.coef)
    #Llamar un elemento
    def __getitem__(self, i):
        return self.coef[i]
    #Suma tradicional
    def __add__(self, v2):
        return Vspace(list(map(lambda a,b:  a+b, self.coef, v2.coef)))
    #Resta
    def __sub__(self, v2):
        return Vspace(list(map(lambda a,b:  a-b, self.coef, v2.coef)))
    #Negativo
    def __neg__(self):
        return Vspace(list(map(lambda a:  -a, self.coef)))
    #Multiplicacion uno a uno
    def __mul__(self, x):
        if type(x) == type(1) or type(x) == type(1.0):
            return Vspace(list(map(lambda y: x*y, self.coef)))
        elif type(self) == type(x):
            return Vspace(list(map(lambda a,b:  a*b, self.coef, x.coef)))
    #Multiplicacion uno a uno    
    def __rmul__(self, x):
        return self * x
    #Potenciacion uno a uno
    def __pow__(self, x):
        if type(x) == type(1) or type(x) == type(1.0):
            return Vspace(list(map(lambda y: y**x, self.coef)))
    #Norma tradicional (Euclidiana)    
    def norm(self, p = 2):
        if type(p) == type(1) or type(p) == type(1.0):
            return (sum(map(lambda x: abs(x) ** p, self.coef)))**(1/p)
        elif p == 'inf':
            return max(self.coef)
     
class Vector(Vspace):
    def __init__(self, coeficientes):
        super().__init__(coeficientes)
     
    def __repr__(self):
        return f'Vector({self.coef})'
     
    def __neg__(self):
        return Vector(super().__neg__().coef)
     
    def __add__(self, v2):
        return Vector(super().__add__(v2).coef)
     
    def __sub__(self, v2):
        return Vector(super().__sub__(v2).coef)
     
    def __rmul__(self, v2):
        return Vector(super().__rmul__(v2).coef)
     
    def __mul__(self, v2):
        return Vector(super().__mul__(v2).coef)
     
    def __pow__(self, x):
        return Vector(super().__pow__(x).coef)
     
    def norm(self, p = 2):
        return super().norm(p)
     
    def dot(self, v2):
        return sum(super().__rmul__(v2))
     
class Polynomial(Vspace):
#Constructor
    def __init__(self, coeficientes):
#Condicion que permite quitar los ceros que estan a la derecha de los polinomios
        while coeficientes[-1]==0:
              coeficientes.pop()
        super().__init__(coeficientes)
         
#metodo que permite ver el los coeficientes del polinomio   
    def __repr__(self):
        return f'Polynomial({self.coef})'
#metodo que permite ver el polinomio opuesto
    def __neg__(self):
        return Polynomial(super().__neg__().coef)
 
#metodo que permite ver la longuitud
    def norm(self, p = 2):
        return super().norm(p)
 
#metodo que permite ver el grado    
    def grado(self):
        return len(self.coef)-1
 
#metodo que permite la multiplicacion de polinomios
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
     
    #funcion que  permitira hallar la exponencial del polinomio
    def __pow__(self,x):
        p=self
        #permitira definir el valor de la exponencial
        for i in range(1,x):
            p=p*self
         
        return p
