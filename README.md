# Tarea2_ProgramacionWeb_ORM
Tarea de programacion web sobre operaciones entre modelos usando el ORM de Django
---------------------------------------------------------------------------------------
Para acceder a la ruta admin con Super Usuario:
Usuario: gloyola
Contraseña: gloyola123

---------------------------------------------------------------------------------------
-------------------------------------------------Scrip de la tarea------------------------------------------------------
(InteractiveConsole)
>>> from tareaorm.models import Producto,Cliente,Factura,DetalleFactura 
>>> producto = Producto.objects.all()  
>>> producto                          
<QuerySet [<Producto: Desinfectante>, <Producto: Supan>, <Producto: Tocino>, <Producto: Deja>, <Producto: Shampoo>, <Producto: Aceite>]>
>>> producto= Producto(descripcion='Pimienton',precio=0.50,stock=1500)       
>>> producto.save()
>>> producto = Producto.objects.all() 
>>> producto
<QuerySet [<Producto: Pimienton>, <Producto: Desinfectante>, <Producto: Supan>, <Producto: Tocino>, <Producto: Deja>, <Producto: Shampoo>, <Producto: Aceite>]>
>>> producto= Producto(descripcion='Gatorade',precio=1.50,stock=500)   
>>> Producto.objects.create(descripcion='Jugo de Manzana',precio=2.80,stock=200)   
<Producto: Jugo de Manzana>
>>> producto= Producto(descripcion='Salsa de Tomate',precio=1.80,stock=1600)  
>>> producto.save()
>>> producto= Producto(descripcion='Jabon',precio=0.80,stock=1000)  
>>> producto.save()
>>> producto= Producto(descripcion='Galletas Amor',precio=1.80,stock=1800)  
>>> producto.save()
>>> Producto.objects.create(descripcion='Zucaritas',precio=3.50,stock=100)
<Producto: Zucaritas>
Inserte dos registros de clientes, 2 registros en el modelo factura con sus dos registros en el modelo detalle Factura con el ejemplo 1 y 2 respectivamente
Dos Registros de clientes
>>> producto= Producto.objects.get(descripcion='Supan')      
>>> producto.descripcion
'Supan'
>>> cliente=Cliente.objects.create(ruc='0985246932',nombre='Ena Nirvana',direccion='Milagro')  
>>> cliente.save()
>>> cliente.producto.add(producto)
>>> cliente=Cliente.objects.all().values('id','nombre','producto') 
>>> cliente
<QuerySet [{'id': 1, 'nombre': 'Gabriela Loyola', 'producto': 1}, {'id': 2, 'nombre': 'Maria Rendon', 'producto': 1}, {'id': 2, 'nombre': 'Maria Rendon', 'producto': 2}, {'id': 3, 'nombre': 'Pedro Jacome', 'producto': 3}, {'id': 4, 'nombre': 'Luisa Salazar', 'producto': 4}, {'id': 5, 'nombre': 'Ana Cobo', 'producto': 5}, {'id': 6, 'nombre': 'Jose Inca', 'producto': 6}, {'id': 7, 'nombre': 'Ena Nirvana', 'producto': 5}]>
>>> cliente=Cliente.objects.create(ruc='0915423988',nombre='Ola Vini',direccion='Vinces')      
>>> cliente.save()
>>> cliente.producto.add(producto)
>>> cliente=Cliente.objects.all().values('id','nombre','producto')
>>> cliente
<QuerySet [{'id': 1, 'nombre': 'Gabriela Loyola', 'producto': 1}, {'id': 2, 'nombre': 'Maria Rendon', 'producto': 1}, {'id': 2, 'nombre': 'Maria Rendon', 'producto': 2}, {'id': 3, 'nombre': 'Pedro Jacome', 'producto': 3}, {'id': 4, 'nombre': 'Luisa Salazar', 'producto': 4}, {'id': 5, 'nombre': 'Ana Cobo', 'producto': 5}, {'id': 6, 'nombre': 'Jose Inca', 'producto': 6}, {'id': 7, 'nombre': 'Ena Nirvana', 'producto': 5}, {'id': 8, 'nombre': 'Ola Vini', 'producto': 5}]>

#Insertar 2 registro en el modelo factura
>>> cliente= Cliente.objects.get(nombre='Ena Nirvana') 
>>> cliente
<Cliente: Ena Nirvana>
>>> factura= Factura(cliente=cliente,fecha='2020-08-04',total=100)
>>> factura.save()
>>> factura= Factura.objects.all().values('id','cliente__nombre') 
>>> factura
<QuerySet [{'id': 1, 'cliente__nombre': 'Gabriela Loyola'}, {'id': 2, 'cliente__nombre': 'Maria Rendon'}, {'id': 3, 'cliente__nombre': 'Pedro Jacome'}, {'id': 4, 'cliente__nombre': 'Luisa Salazar'}, {'id': 5, 'cliente__nombre': 'Ana Cobo'}, {'id': 6, 'cliente__nombre': 'Jose Inca'}, {'id': 7, 'cliente__nombre': 'Ena Nirvana'}]>
>>> clientes=Cliente.objects.all().values('id','nombre','direccion') 
>>> clientes
<QuerySet [{'id': 1, 'nombre': 'Gabriela Loyola', 'direccion': 'Guayaquil'}, {'id': 2, 'nombre': 'Maria Rendon', 'direccion': 'Carchi'}, {'id': 3, 'nombre': 'Pedro Jacome', 'direccion': 'Rocafuerte'}, {'id': 4, 'nombre': 'Luisa Salazar', 'direccion': 'Carchi'}, {'id': 5, 'nombre': 'Ana Cobo', 'direccion': 'Guayaquil'}, {'id': 6, 'nombre': 'Jose Inca', 'direccion': 'Jujan'}, {'id': 7, 'nombre': 'Ena Nirvana', 'direccion': 'Milagro'}, {'id': 8, 'nombre': 'Ola Vini', 'direccion': 'Vinces'}]>
>>> clientes=Cliente.objects.get(id=2)
>>> factura= Factura.objects.create(cliente=cliente,fecha='2020-08-04',total=200)   
>>> factura= Factura.objects.all().values('id','cliente__nombre') 
>>> factura
<QuerySet [{'id': 1, 'cliente__nombre': 'Gabriela Loyola'}, {'id': 2, 'cliente__nombre': 'Maria Rendon'}, {'id': 3, 'cliente__nombre': 'Pedro Jacome'}, {'id': 4, 'cliente__nombre': 'Luisa Salazar'}, {'id': 5, 'cliente__nombre': 'Ana Cobo'}, {'id': 6, 'cliente__nombre': 'Jose Inca'}, {'id': 7, 'cliente__nombre': 'Ena Nirvana'}, {'id': 8, 'cliente__nombre': 'Ena Nirvana'}]>

#Insertar 2 registros en el detalle de factura
>>> factura= Factura.objects.get(cliente__nombre='Pedro Jacome') 
>>> factura
<Factura: Pedro Jacome>
>>> factura.fecha
datetime.date(2020, 8, 5)
>>> producto = Producto.objects.get(descripcion='Pimienton')        
>>> producto
<Producto: Pimienton>
>>> DetalleFactura.objects.create(factura=factura,producto=producto,cantidad=10,precio=0.50,subtotal=10*0.50) 
<DetalleFactura: DetalleFactura object (1)>
>>> producto = Producto.objects.get(descripcion='Tocino')    
>>> DetalleFactura.objects.create(factura=factura,producto=producto,cantidad=15,precio=4.50,subtotal=15*4.50) 
<DetalleFactura: DetalleFactura object (2)>
>>> factura= Factura.objects.get(cliente__nombre='Luisa Salazar')        
>>> producto = Producto.objects.get(descripcion='Supan')  
>>> DetalleFactura.objects.create(factura=factura,producto=producto,cantidad=20,precio=1.80,subtotal=20*1.80) 
<DetalleFactura: DetalleFactura object (3)>
>>> producto = Producto.objects.get(descripcion='Supan')
>>> detalle= DetalleFactura(factura=factura,producto=producto,cantidad=25,precio=1.80,subtotal=25*1.80)
>>> detalle.save()
>>> detalle=DetalleFactura.objects.all().values('factura__id','factura__cliente__nombre','producto__descripcion','cantidad','precio') 
>>> detalle
<QuerySet [{'factura__id': 3, 'factura__cliente__nombre': 'Pedro Jacome', 'producto__descripcion': 'Pimienton', 'cantidad': 10.0, 'precio': 0.5}, {'factura__id': 3, 'factura__cliente__nombre': 'Pedro Jacome', 'producto__descripcion': 'Tocino', 'cantidad': 15.0, 'precio': 4.5}, {'factura__id': 4, 'factura__cliente__nombre': 'Luisa Salazar', 'producto__descripcion': 'Supan', 'cantidad': 20.0, 'precio': 1.8}, {'factura__id': 4, 'factura__cliente__nombre': 'Luisa Salazar', 'producto__descripcion': 'Supan', 'cantidad': 25.0, 'precio': 1.8}]>

#Actualizar registros en los modelos
>>> producto= Producto.objects.get(descripcion='Shampoo')
>>> producto.precio
2.8
>>> producto.precio= 3.80
>>> producto.save()
>>> producto.descripcion
'Shampoo'
>>> producto.precio       
3.8
>>> Producto.objects.filter(descripcion='Shampoo').update(precio= 4.00)
1

#Modificar 2 registros de producto, cliente, factura y detalleFactura con el ejemplo 1 y 2 respectivamente
#Modificar 2 registro de producto
>>> producto= Producto.objects.get(id=3)  
>>> producto.descripcion
'Deja'
>>> producto.precio     
1.0
>>> producto.precio= 1.20
>>> producto.save()      
>>> producto.descripcion  
'Deja'
>>> producto.precio       
1.2
>>> Producto.objects.filter(descripcion='Deja').update(precio=1.40)   
1

#Modificar 2 registros de cliente
>>> cliente= Cliente.objects.get(id=5) 
>>> cliente.nombre
'Ana Cobo'
>>> cliente.direccion
'Guayaquil'
>>> cliente.direccion= 'Bucay'
>>> cliente.save()
>>> cliente= Cliente.objects.get(id=6) 
>>> cliente.nombre    
'Jose Inca'
>>> cliente.direccion
'Jujan'
>>> cliente.direccion= 'Pedro Carbo'
>>> cliente.save()
>>> cliente.nombre    
'Jose Inca'
>>> cliente.direccion
'Pedro Carbo'
>>> Cliente.objects.filter(nombre='Jose Inca').update(direccion= 'Samborondon')          
1

#Modificar 2 registros de factura
>>> cliente=Cliente.objects.get(id=8)
>>> cliente.nombre 
'Ola Vini'
>>> Factura.objects.filter(cliente__nombre='Ana Cobo').update(cliente=cliente)   
1
>>> Factura.objects.all().values('id','cliente__nombre','fecha')  
<QuerySet [{'id': 1, 'cliente__nombre': 'Gabriela Loyola', 'fecha': datetime.date(2020, 8, 1)}, {'id': 2, 'cliente__nombre': 'Maria Rendon', 'fecha': datetime.date(2020, 8, 5)}, {'id': 3, 'cliente__nombre': 'Pedro Jacome', 'fecha': datetime.date(2020, 8, 5)}, {'id': 4, 'cliente__nombre': 'Luisa Salazar', 
'fecha': datetime.date(2020, 8, 3)}, {'id': 5, 'cliente__nombre': 'Ola Vini', 'fecha': datetime.date(2020, 8, 2)}, {'id': 6, 'cliente__nombre': 'Jose Inca', 'fecha': datetime.date(2020, 8, 5)}, {'id': 7, 'cliente__nombre': 'Ena Nirvana', 'fecha': datetime.date(2020, 8, 4)}, {'id': 8, 'cliente__nombre': 'Ena Nirvana', 'fecha': datetime.date(2020, 8, 4)}]>
>>> cliente= Cliente.objects.get(nombre='Jose Inca') 
>>> factura= Factura.objects.get(cliente=cliente)
>>> factura
<Factura: Jose Inca>
>>> cliente.id
6
>>> cliente= Cliente.objects.get(nombre='Ena Nirvana')
>>> factura.cliente=cliente
>>> factura.save()
>>> Factura.objects.all().values('id','cliente__nombre','fecha')
<QuerySet [{'id': 1, 'cliente__nombre': 'Gabriela Loyola', 'fecha': datetime.date(2020, 8, 1)}, {'id': 2, 'cliente__nombre': 'Maria Rendon', 'fecha': datetime.date(2020, 8, 5)}, {'id': 3, 'cliente__nombre': 'Pedro Jacome', 'fecha': datetime.date(2020, 8, 5)}, {'id': 4, 'cliente__nombre': 'Luisa Salazar', 
'fecha': datetime.date(2020, 8, 3)}, {'id': 5, 'cliente__nombre': 'Ola Vini', 'fecha': datetime.date(2020, 8, 2)}, {'id': 6, 'cliente__nombre': 'Ena Nirvana', 'fecha': datetime.date(2020, 8, 5)}, {'id': 7, 'cliente__nombre': 'Ena Nirvana', 'fecha': datetime.date(2020, 8, 4)}, {'id': 8, 'cliente__nombre': 
'Ena Nirvana', 'fecha': datetime.date(2020, 8, 4)}]>

#Modificar 2 registro de DetalleFactura
>>> detalle=DetalleFactura.objects.all().values('factura__id','factura__cliente__nombre','producto__descripcion','cantidad','precio')
>>> detalle
<QuerySet [{'factura__id': 3, 'factura__cliente__nombre': 'Pedro Jacome', 'producto__descripcion': 'Pimienton', 'cantidad': 10.0, 'precio': 0.5}, {'factura__id': 3, 'factura__cliente__nombre': 'Pedro Jacome', 'producto__descripcion': 'Tocino', 'cantidad': 15.0, 'precio': 4.5}, {'factura__id': 4, 'factura__cliente__nombre': 'Luisa Salazar', 'producto__descripcion': 'Supan', 'cantidad': 20.0, 'precio': 1.8}, {'factura__id': 4, 'factura__cliente__nombre': 'Luisa Salazar', 'producto__descripcion': 'Supan', 'cantidad': 25.0, 'precio': 1.8}, {'factura__id': 1, 'factura__cliente__nombre': 'Gabriela Loyola', 'producto__descripcion': 'Tocino', 'cantidad': 2.0, 'precio': 4.5}]>
>>> producto = Producto.objects.get(descripcion='Desinfectante')   
>>> factura = Factura.objects.get(id=1) 
>>> DetalleFactura.objects.filter(producto__descripcion='Tocino').update(producto=producto)       
2
>>> detalle= DetalleFactura.objects.all().values('factura__id','factura__cliente__nombre','producto__descripcion','cantidad','precio')
>>> detalle
<QuerySet [{'factura__id': 3, 'factura__cliente__nombre': 'Pedro Jacome', 'producto__descripcion': 'Pimienton', 'cantidad': 10.0, 'precio': 0.5}, {'factura__id': 3, 'factura__cliente__nombre': 'Pedro Jacome', 'producto__descripcion': 'Desinfectante', 'cantidad': 15.0, 'precio': 4.5}, {'factura__id': 4, 'factura__cliente__nombre': 'Luisa Salazar', 'producto__descripcion': 'Supan', 'cantidad': 20.0, 'precio': 1.8}, {'factura__id': 4, 'factura__cliente__nombre': 'Luisa Salazar', 'producto__descripcion': 'Supan', 'cantidad': 25.0, 'precio': 1.8}, {'factura__id': 1, 'factura__cliente__nombre': 'Gabriela Loyola', 'producto__descripcion': 'Desinfectante', 'cantidad': 2.0, 'precio': 4.5}]>
>>> producto = Producto.objects.get(descripcion='Shampoo')         
>>> factura = Factura.objects.get(id=1)
>>> detalle= DetalleFactura.objects.get(factura=factura)   
>>> detalle.producto= producto
>>> detalle.save()
>>> detalle= DetalleFactura.objects.all().values('factura__id','factura__cliente__nombre','producto__descripcion','cantidad','precio')
>>> detalle
<QuerySet [{'factura__id': 3, 'factura__cliente__nombre': 'Pedro Jacome', 'producto__descripcion': 'Pimienton', 'cantidad': 10.0, 'precio': 0.5}, {'factura__id': 3, 'factura__cliente__nombre': 'Pedro Jacome', 'producto__descripcion': 'Desinfectante', 'cantidad': 15.0, 'precio': 4.5}, {'factura__id': 4, 'factura__cliente__nombre': 'Luisa Salazar', 'producto__descripcion': 'Supan', 'cantidad': 20.0, 'precio': 1.8}, {'factura__id': 4, 'factura__cliente__nombre': 'Luisa Salazar', 'producto__descripcion': 'Supan', 'cantidad': 25.0, 'precio': 1.8}, {'factura__id': 1, 'factura__cliente__nombre': 'Gabriela Loyola', 'producto__descripcion': 'Shampoo', 'cantidad': 2.0, 'precio': 4.5}]>

#Eliminar registros en los modelos
>>> producto = Producto.objects.get(id=8)  
>>> producto.descripcion
'Jugo de Manzana'
>>> producto.delete()
(1, {'tareaorm.Producto': 1})
>>> Producto.objects.filter(descripcion='Supan').delete()     
(6, {'tareaorm.Cliente_producto': 3, 'tareaorm.DetalleFactura': 2, 'tareaorm.Producto': 1})

#Querys en un modelo
>>> producto=Producto.objects.all()  
>>> producto
<QuerySet [<Producto: Zucaritas>, <Producto: Galletas Amor>, <Producto: Jabon>, <Producto: Salsa de Tomate>, <Producto: Pimienton>, <Producto: Desinfectante>, <Producto: Tocino>, <Producto: Deja>, <Producto: Shampoo>, <Producto: Aceite>]>
>>> producto=Producto.objects.get(id=9) 
>>> producto
<Producto: Salsa de Tomate>
>>> Producto.objects.filter(id__lte=6) 
<QuerySet [<Producto: Desinfectante>, <Producto: Tocino>, <Producto: Deja>, <Producto: Shampoo>, <Producto: Aceite>]>
>>> Producto.objects.exclude(descripcion__icontains='Salsa')     
<QuerySet [<Producto: Zucaritas>, <Producto: Galletas Amor>, <Producto: Jabon>, <Producto: Pimienton>, <Producto: Desinfectante>, <Producto: Tocino>, <Producto: Deja>, <Producto: Shampoo>, <Producto: Aceite>]>
>>> Producto.objects.filter(id__gte=3)  
<QuerySet [<Producto: Zucaritas>, <Producto: Galletas Amor>, <Producto: Jabon>, <Producto: Salsa de Tomate>, <Producto: Pimienton>, <Producto: Desinfectante>, <Producto: Tocino>, <Producto: Deja>]>
>>> Producto.objects.filter(id__gt=3).values('id','descripcion')  
<QuerySet [{'id': 12, 'descripcion': 'Zucaritas'}, {'id': 11, 'descripcion': 'Galletas Amor'}, {'id': 10, 'descripcion': 'Jabon'}, {'id': 9, 'descripcion': 'Salsa de Tomate'}, {'id': 7, 'descripcion': 'Pimienton'}, {'id': 6, 'descripcion': 'Desinfectante'}, {'id': 4, 'descripcion': 'Tocino'}]>
>>> Producto.objects.filter(id__lt=4).values('id','descripcion')  
<QuerySet [{'id': 3, 'descripcion': 'Deja'}, {'id': 2, 'descripcion': 'Shampoo'}, {'id': 1, 'descripcion': 'Aceite'}]>
>>> Producto.objects.filter(descripcion='Pimienton').values('id','descripcion')
<QuerySet [{'id': 7, 'descripcion': 'Pimienton'}]>

#Querys de varios modelos (relacionados)
>>> Factura.objects.filter(cliente__nombre='Ola Vini')       
<QuerySet [<Factura: Ola Vini>]>
>>> clientes.factura_set.all() 
<QuerySet [<Factura: Maria Rendon>]>
>>> Factura.objects.select_related('cliente').filter(cliente__nombre='Ola Vini')       
<QuerySet [<Factura: Ola Vini>]>
>>> Cliente.objects.prefetch_related('producto').filter(nombre='Gabriela Loyola').values('nombre','producto__descripcion')  
<QuerySet [{'nombre': 'Gabriela Loyola', 'producto__descripcion': 'Aceite'}]>

