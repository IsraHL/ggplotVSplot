# ggplotVSplot

## Introducción

En este repositorio se realizaran algunas comparaciones entre las gráficas de la paqueteria ggplot y las gráficas por default que presenta R. También se abordará la manera en que puedes mejorar el estilo de cada una de ellas, desde cambiar el tamaño y tipo de letra, el color de la grafica, agregar notas entre algunas otras cosas. Aunque las mejoras que se proponen respecto al estilo son ciertamente casi identicas para todas las gráficas, siempre se incluiran en el código de las mismas, de esta manera cuando se quiera buscar una gráfica se puedan observar un código lo más completo posible. 

Recordemos la instalación de ggplot

```[R project]
install.packages('ggplot2')
library('ggplot2')
```

## Gráfica de Puntos (Scatterplott).

Ocuparemos la libreria *Iris*.

```[R project, echo= T]
head(iris)
```
Con ggplot tenemos :
```[R project, echo= T]
ggplot(iris, aes(x=Sepal.Length, y=Sepal.Width)) + geom_point()
```
![ggplot Iris](https://github.com/IsraHL/ggplotVSplot/blob/master/Ggpoints.jpg)

Con el código natural:
```[R project, echo= T]
plot(iris$Sepal.Length, iris$Sepal.Width)
```

![plot Iris](https://github.com/IsraHL/ggplotVSplot/blob/master/plotpoints.jpeg)

Contemplando 5 variables tenemos y agregando una presentación más estilizada tenemos:

```[R project, echo= T]
ggplot(iris, aes(x=Sepal.Length, y=Sepal.Width, color=Petal.Length, size=Petal.Length, shape=Species)) + 
    geom_point(alpha=0.6)+ #alpha nos brinda la posibilidad de aclarar el color de los puntos
    theme_minimal()+ 
    #cambia el tipo de tema en ggplot, algunos otros son theme_bw(), theme_grey(), theme_minimal(), theme_classic().
    theme(legend.position = "none")+ #Quita la legenda de la gráfica
    scale_shape_manual(values = c(15,17,19))+
    scale_colour_gradientn(colours = terrain.colors(10))+  #Cambiar la escala de color
    theme (text = element_text(size=11)) + # Tamaño de fuente del grafico por defecto
    ggtitle ("Data Iris") +
    theme(plot.title= element_text(size=rel(3), #Tamaño relativo de la letra del título
             vjust=2, #Justificación vertical para separarlo del gráfico
             face="bold.italic", #Letra negrilla Otras posibilidades "plain" "italic" "bold" y "bold.italic"
             color="grey11", #Color del texto
             lineheight=1.5  #Separación entre líneas
             )) + 
    labs(x = "Sepal Length", y = "Sepal Width") + #Titulos de los ejes
    theme( axis.text.x = element_text(face="bold.italic", colour="grey6", size=rel(1)),
    axis.text.y = element_text(face="bold.italic", colour="grey6", size=rel(1), angle=0, hjust=0.5))+
    geom_smooth(method="loess", alpha=0.1, se = T, col="grey80")
```
![plot Iris](https://github.com/IsraHL/ggplotVSplot/blob/master/Ggpoints2.jpeg)

Por otro lado con el código default tenemos:
```[R project, echo= T]
    setosa.=iris[iris$Species=="setosa",]
    versicolor.=iris[iris$Species=="versicolor",]
    virginica.=iris[iris$Species=="virginica",]
    plot(c(4,8),c(2,4.5),type="n",main="Data Iris",  xlab="Sepal Length", ylab="Sepal Width")
    points(setosa.$Sepal.Length,setosa.$Sepal.Width,
        cex= setosa.$Petal.Length, #Tamaño
        col=rgb(red=0, green=setosa.$Petal.Length/1.9, blue=0, alpha=.3),
        pch=15)
    points(versicolor.$Sepal.Length,versicolor.$Sepal.Width,
        cex= versicolor.$Petal.Length, #Tamaño
        col=rgb(red=versicolor.$Petal.Length/5.1, green=versicolor.$Petal.Length/5.1, blue=0, alpha=.3),
        pch=17)
     points(virginica.$Sepal.Length,virginica.$Sepal.Width,
        cex= virginica.$Petal.Length, #Tamaño
        col=rgb(red=virginica.$Petal.Length/6.9, green=0, blue=virginica.$Petal.Length/6.9, alpha=.3),
        pch=16)    

    medelosetosa=loess(formula = Sepal.Width ~ Sepal.Length, data = setosa.) 
    myPredict <- predict( modelosetosa , interval="predict" )
    ix <- sort(setosa.$Sepal.Length,index.return=T)$ix
    lines(setosa.$Sepal.Length[ix], myPredict[ix , 1], col='gray80', lwd=1 )  
    polygon(c(rev(setosa.$Sepal.Length[ix]), setosa.$Sepal.Length[ix]), c(rev(myPredict[ ix,3]), myPredict[ ix,2]), 
            col = rgb(0.7,0.7,0.7,0.4) , border = NA)  
    medeloversicolor=loess(formula = Sepal.Width ~ Sepal.Length, data = versicolor.) 
    myPredict <- predict( modeloversicolor , interval="predict" )
    ix <- sort(versicolor.$Sepal.Length,index.return=T)$ix
    lines(versicolor.$Sepal.Length[ix], myPredict[ix , 1], col='gray80', lwd=1 )  
    polygon(c(rev(versicolor.$Sepal.Length[ix]), versicolor.$Sepal.Length[ix]), c(rev(myPredict[ ix,3]), myPredict[ ix,2]), 
            col = rgb(0.7,0.7,0.7,0.4) , border = NA)
    medelovirginica=loess(formula = Sepal.Width ~ Sepal.Length, data = virginica.) 
    myPredict <- predict( modelovirginica , interval="predict" )
    ix <- sort(virginica.$Sepal.Length,index.return=T)$ix
    lines(virginica.$Sepal.Length[ix], myPredict[ix , 1], col='gray80', lwd=1 )  
    polygon(c(rev(virginica.$Sepal.Length[ix]), virginica.$Sepal.Length[ix]), c(rev(myPredict[ ix,3]), myPredict[ ix,2]), 
            col = rgb(0.7,0.7,0.7,0.4) , border = NA)
           
```




