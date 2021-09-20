<template>
    <div>
        <div>
            <h1 class="text-center textocolor fredoka mt-5 pt-4">Crear Grafo</h1>
            <div class="row justify-content-center">
                <div class="grafo1 col-md-5 card cardaux mr-3">
                    <div class="row ml-1 my-3">
                        <div class="container-fluid mr-4">
                            <h3>Seleccione el tipo de grafo:</h3>
                            <select class="custom-select  mb-3 mr-3 mt-2" v-model="option">
                                <option selected :value="0">Seleccione un tipo de grafo:</option>
                                <option :value="1">Grafo simple /no dirigido</option>
                                <option :value="2">Grafo simple /dirigido </option>
                                <option :value="3">Grafo dirigido /etiquetado</option>  
                                <option :value="4">Grafo no dirigido /etiquetado</option>   
                            </select> 
                        </div>
                        <div class="container-fluid py-4 mr-4" v-if="option===1">
                            <h3 class="mt-2">Grafo simple No dirigido</h3>
                            <hr>
                            <div class="row text-center">
                                <div class="col-md-4">
                                    <button class="btn btn-success" @click="createNode"><i class="fa fa-plus"></i>Añadir nodo</button>
                                </div>
                                <div class="col-md-4">
                                    <button type="button" class="btn btn-success" @click="createArista"><i class="fa fa-plus"></i>Añadir arista</button>
                                </div>
                                <div class="col-md-4">
                                    <button class="btn btn-danger" @click="delAndClear"><i class="fa fa-remove"></i>Eliminar Grafo</button>
                                </div>
                            </div>
                            <div v-if="create" class="my-3">
                                <div>
                                    <form @submit.prevent="crearNodo">
                                        <div class="form-group">
                                            <label for="id">Ingrese ID de nodo: </label> 
                                            <input type="number" min="1" v-model="nodo.id" name="id" class="form-control"> 
                                        </div>

                                        <button class="btn btn-success btn-sm" type="submit">Agregar</button>
                                    </form>       
                                </div>
                            </div>
                            <div v-if="createAris" class="my-3">
                                <form @submit.prevent="crearArista">
                                    <div class="form-group">
                                        <label>Ingrese nodo desde el cual sale la arista:</label>
                                        <input type="number" min="1" v-model="arista.from" class="form-control"> 
                                    </div>
                                    <div class="form-group">
                                        <label>Ingrese nodo al cual llega la arista:</label>
                                        <input type="number" min="1" v-model="arista.to" class="form-control"> 
                                    </div>
                            
                                    <button class="btn btn-success btn-sm" type="submit" >Agregar</button>
                                    <button class="btn btn-success btn-sm" @click="drawGrafo">Dibujar Grafo</button>
                                </form>
                            </div>
                        </div>

                        <div class="container-fluid py-4 mr-4" v-if="option===2">
                            <div>
                                <h3 class="mt-2">Grafo simple dirigido</h3> 
                                <hr>
                                <div class="row text-center">
                                    <div class="col-md-4">
                                        <button class="btn btn-success" @click="createNode">Añadir nodo</button>
                                    </div>
                                    <div class="col-md-4">
                                        <button class="btn btn-success" @click="createArista">Añadir arista</button>
                                    </div>
                                    <div class="col-md-4">
                                        <button class="btn btn-danger" @click="delAndClear">Eliminar Grafo</button>
                                    </div>
                                </div>

                                    <div v-if="create" class="my-3">
                                        <div>
                                            <form @submit.prevent="crearNodo">
                                                <div class="form-group">
                                                    <label for="id">ingrese el id: </label> 
                                                    <input type="number" min="1" v-model="nodo.id" name="id" class="form-control"> 
                                                </div>

                                                <button class="btn btn-success btn-sm" type="submit">Agregar</button>
                                            </form>       
                                        </div>
                                    </div>

                                    <div v-if="createAris" class="my-3">
                                        <form @submit.prevent="crearArista">
                                            <div class="form-group">
                                                <label>Ingrese nodo desde el cual sale la arista:</label>
                                                <input type="number" min="1" v-model="aristaDirigido.from" class="form-control"> 
                                            </div>
                                            <div class="form-group">
                                                <label>Ingrese nodo al cual llega la arista:</label>
                                                <input type="number" min="1" v-model="aristaDirigido.to" class="form-control"> 
                                            </div>
                                    
                                            <button class="btn btn-success btn-sm" type="submit" >Agregar</button>
                                            <button class="btn btn-success btn-sm" @click="drawGrafoDirigido">dibujar</button>
                                        </form>
                                    </div>
                            </div>
                        </div>

                        <div class="container-fluid py-4 mr-4" v-if="option===3">
                            <div>
                                <h3 class="mt-2">Grafo Dirigido Etiquetado</h3>
                                <hr>

                                    <div class="row text-center">
                                        <div class="col-md-4">
                                            <button class="btn btn-success" @click="createNode">Añadir nodo</button>
                                        </div>
                                        <div class="col-md-4">
                                            <button class="btn btn-success" @click="createArista">Añadir arista</button>
                                        </div>
                                        <div class="col-md-4">
                                            <button class="btn btn-danger" @click="delAndClear">Eliminar Grafo</button>
                                        </div>
                                    </div>
                                    <div v-if="create" class="my-3">
                                        <div>
                                            <form @submit.prevent="crearNodo">
                                                <div class="form-group">
                                                    <label for="id">ingrese el id: </label> 
                                                    <input type="number" min="1" v-model="nodo.id" name="id" class="form-control"> 
                                                </div>

                                                <button class="btn btn-success btn-sm" type="submit">Agregar</button>
                                            </form>       
                                        </div>
                                    </div>
                                    <div v-if="createAris" class="my-3">
                                        <form @submit.prevent="crearArista">
                                            <div class="form-group">
                                                <label>Ingrese nodo desde el cual sale la arista:</label>
                                                <input type="number" min="1" v-model="aristaEtiquetadaDirigida.from" class="form-control"> 
                                            </div>
                                            <div class="form-group">
                                                <label>Ingrese nodo al cual llega la arista:</label>
                                                <input type="number" min="1" v-model="aristaEtiquetadaDirigida.to" class="form-control"> 
                                            </div>
                                            <div class="form-group">
                                                <label>Ingrese el peso de la arista: </label>
                                                <input type="number" v-model="aristaEtiquetadaDirigida.label" class="form-control">
                                            </div>
                                    
                                            <button class="btn btn-success btn-sm" type="submit" >Agregar</button>
                                            <button class="btn btn-success btn-sm" @click="drawGrafo">dibujar</button>
                                        </form>
                                    </div>

                            </div>

                        </div>

                        <div class="container-fluid py-4 mr-4" v-if="option===4">
                            <div>
                                <h3 class="mt-2">Grafo No Dirigido Etiquetado</h3>
                                <hr>

                                    <div class="row text-center">
                                        <div class="col-md-4">
                                            <button class="btn btn-success" @click="createNode">Añadir nodo</button>
                                        </div>
                                        <div class="col-md-4">
                                            <button class="btn btn-success" @click="createArista">Añadir arista</button>
                                        </div>
                                        <div class="col-md-4">
                                            <button class="btn btn-danger" @click="delAndClear">Eliminar Grafo</button>
                                        </div>
                                    </div>
                                    <div v-if="create" class="my-3">
                                        <div>
                                            <form @submit.prevent="crearNodo">
                                                <div class="form-group">
                                                    <label for="id">ingrese el id: </label> 
                                                    <input type="number" min="1" v-model="nodo.id" name="id" class="form-control"> 
                                                </div>

                                                <button class="btn btn-success btn-sm" type="submit">Agregar</button>
                                            </form>       
                                        </div>
                                    </div>
                                    <div v-if="createAris" class="my-3">
                                        <form @submit.prevent="crearArista">
                                            <div class="form-group">
                                                <label>Ingrese nodo desde el cual sale la arista:</label>
                                                <input type="number" min="1" v-model="aristaEtiquetada.from" class="form-control"> 
                                            </div>
                                            <div class="form-group">
                                                <label>Ingrese nodo al cual llega la arista:</label>
                                                <input type="number" min="1" v-model="aristaEtiquetada.to" class="form-control"> 
                                            </div>
                                            <div class="form-group">
                                                <label>Ingrese el peso de la arista: </label>
                                                <input type="number" v-model="aristaEtiquetada.label" class="form-control">
                                            </div>
                                    
                                            <button class="btn btn-success btn-sm" type="submit" >Agregar</button>
                                            <button class="btn btn-success btn-sm" @click="drawGrafo">dibujar</button>
                                        </form>
                                    </div>

                            </div>

                        </div>
                    </div>
                </div>
            </div>                                                 
            <div class="row justify-content-center">
                <h3 class="text-center fredoka my-2">Graficacion</h3>
                <div id="grafo" class="mb-3" style="border: 1px solid lightgray;"></div>
            </div>
            <h1 class="text-center fredoka textocolor my-4">Informacion del Grafo</h1>
            <div class="row justify-content-center">
                <div class="card cardaux4 col-md-10 rounded-top">
                    <div class="btn-group justify-content-center" role="group">
                        <a href="#matrizcaminos"><button type="button" class="btn btn-secondary" @click="mostrarOp1">Matriz de caminos</button></a>
                        <a href="#caminocorto"><button type="button" class="btn btn-secondary" @click="mostrarOp2">Camino más corto</button></a>
                        <a href="#hamiltoniano"><button type="button" class="btn btn-secondary" @click="mostrarOp3">Hamiltoniano / Euleriano</button></a>
                        <a href="#arbolgenerador"><button type="button" class="btn btn-secondary" @click="mostrarOp5">Arbol Generador</button></a>
                    </div>
                </div>

                <div class="cardaux2 col-md-10" v-if="controlanalisis==1">
                    <h3 class="text-center fredoka textocolor my-3">Matriz de caminos</h3>
                </div>
                <div id="matrizcaminos" class="card cardaux3 col-md-10 rounded-bottom mb-3" v-if="controlanalisis==1">
                    <div class="container">
                        <div class="container my-3">
                            
                            <div v-if="esConexo">
                                <h5>Este grafo <b>es Conexo</b></h5> 
                            </div>
                            <div v-else>
                                <h5>Este grafo <b>no es Conexo</b></h5> 
                            </div>
                            <div class="row">
                                <div class="col-md-6">
                                    <h4 class="text-center fredoka textocolor my-3">Matriz de Adyacencia</h4>
                                    <table class="table table-dark text-center">
                                        <tr v-for="(item, index) in Adyacencia"  :key="index">
                                            <td v-for="(indice,indiceAdyacencia) in item" :key="indiceAdyacencia">
                                                {{indice}}
                                            </td>
                                        </tr>
                                    </table>
                                </div>
                                <div class="col-md-6">
                                    <h4 class="text-center fredoka textocolor my-3">Matriz de caminos</h4>
                                    <table class="table table-dark text-center">
                                        <tr v-for="(item, index) in matrixCaminos"  :key="index">
                                            <td v-for="(indice,indicecaminos) in item" :key="indicecaminos">
                                                {{indice}}
                                            </td>
                                        </tr>
                                    </table>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="cardaux2 col-md-10" v-if="controlanalisis==2">
                    <h3 class="text-center fredoka textocolor my-3">Camino más corto</h3>
                </div>
                <div id="caminocorto" class="card cardaux3 col-md-10 rounded-bottom" v-if="controlanalisis==2">
                    <div class="container">
                        Camino mas corto
                        (No funciona con grafos simples)
                        <div>

                            <form @submit.prevent="caminoCorto">
                                <label>Ingrese id de nodo de inicio: </label>
                                <input type="number" min="1" v-model="inicio" class="form-control">
                        
                                <button>Consultar</button>
                            </form>
                        </div>

                        <div>
                            Los caminos mínimos desde el nodo de inicio son:
                            <div class="row">
                                <div class="col-md-4"></div>
                                <div class="col-md-4">
                                    <div v-for="(item,index) in getDijkstra" :key="index">
                                          <b> camino n° {{index+1}}:</b> {{inicio}}
                                        <span v-for="(elemento,indice) in item" :key="indice">
                                            {{elemento}}
                                        </span>
                                    </div>
                                </div>
                                <div class="col-md-4"></div>
                            </div>         
                        </div>
                    </div>
                </div>

                <div class="cardaux2 col-md-10" v-if="controlanalisis==3">
                    <h3 class="text-center fredoka textocolor my-3">Hamiltoniano / Euleriano</h3>
                </div>
                <div id="hamiltoniano" class="card cardaux3 col-md-10 rounded-bottom" v-if="controlanalisis==3">
                    <div class="container">
                        Hamiltoniano / Euleriano
                        
                        <div class="container">
                            <div class="">
                                <div v-if="controlanalisis==3">
                                    <div v-if="euler">
                                        Este grafo es Euleriano.
                                        <div class="form-group">
                                            <form @submit.prevent="graficarCircuitoEuleriano">
                                                <label>Ingrese id de nodo de inicio: </label>
                                                <input type="number" min="1" v-model="eleccion" class="form-control">
                                                <div class="justify-content-center">
                                                    <button class="btn btn-success m-3">Consultar</button>
                                                </div>
                                            </form>
                                        </div>
                                        
                                        <div class="mb-4">
                                            Este es el ciclo Euleriano
                                            {{arregloEuleriano}}
                                        </div>
                                    </div>
                                    <div v-else-if="!euler">
                                        Este Grafo no es Euleriano.
                                    </div>
                                </div>
                                <div v-if="controlanalisis==3">
                                    <div v-if="isHamiltoniano">
                                        Este Grafo es Hamiltoniano.
                                        <div class="form-group">
                                            <form @submit.prevent="isHamiltoniano">
                                                <label>Ingrese id de nodo de inicio: </label>
                                                <input type="number" min="1" v-model="eleccion" class="form-control">
                                                <div class="justify-content-center">
                                                    <button class="btn btn-success m-3">Consultar</button>

                                                </div>
                                            </form>
                                        </div>
                                    <div class="mb-4">
                                        Este es el ciclo Hamiltoniano
                                        {{hamilton}}
                                    </div>
                                    </div>
                                    <div v-else-if="!isHamiltoniano">
                                        Este Grafo no es Hamiltoniano.
                                    </div>

                                </div>

                                <div >
                                    
                                    
                                </div>

                            </div>
                        </div>
                    </div>
                </div>

                <div class="cardaux2 col-md-10" v-if="controlanalisis==4">
                    <h3 class="text-center fredoka textocolor my-3">Flujo Máximo</h3>
                </div>
                <div id="flujomaximo" class="card cardaux3 col-md-10 rounded-bottom" v-if="controlanalisis==4">
                    <div class="container">
                        Flujo Maximo
                    </div>
                </div>

                <div class="cardaux2 col-md-10" v-if="controlanalisis==5">
                    <h3 class="text-center fredoka textocolor my-3">Árbol Generador</h3>
                    <div class="row text-center mb-3">
                        
                        <div class="col-md-4"></div>
                        <div class="col-md-4 align-items-center">
                            <div class="text-center">
                                <button class="btn btn-dark" @click="mostrarArbol" >Mostrar Árbol</button>
                            </div>
                        </div>
                        <div class="col-md-4"></div>
                        
                        
                    </div>
                    
                    
                </div>
                <div id="arbolgenerador" class="card cardaux3 col-md-10 rounded-bottom" v-if="controlanalisis==5">
                    <div class="container">
                        <h3 class="text-center fredoka my-3">Árbol Mínimo Generado</h3>
                        <div id="arbol" class="grafo1 my-3">
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </div>
</template>

<script>

import vis from 'vis'

export default {
    data(){
        console.log('Inicia la creacion de la data');
        return{
            nodo:{id:'', label:'',color:'#0BC596'},
            arista:{from:'',to:'',color:{color:'rgb(0,0,0)'},font:{color:'rgb(255,255,255)'}},
            aristaDirigido:{from:'', to:'', color:{color:'rgb(0,0,0)'},font:{color:'rgb(255,255,255)'}},
            aristaEtiquetada:{from:'', to:'', label:'',color:{color:'rgb(0,0,0)'},font:{color:'rgb(255,255,255)'}},
            aristaEtiquetadaDirigida:{from:'', to:'', label:'',color:{color:'rgb(0,0,0)'},font:{color:'rgb(255,255,255)'}},
            
            nodos:[],   
            aristas:[],
            matrixCaminos:[],
            euler:'',
            hamilton:[],
            eleccion:'',
            matrizcostos:[],
            Adyacencia:[],
            caminoPrim:[],
            dijkstra:[],
            caminosDijsktra:[],
            getDijkstra:[],
            inicio:'',
            iniciodijs:'',
            esConexo:'',
            
            addgrafo: false,
            option:'',
            create:false,
            createAris:false,
            controlanalisis: '',
            arregloEuleriano:[],
        }
    }, 
    created(){
        console.log('Data Creada');
        this.prim()
        
    },

    

    methods:{
        llamarHam(){
            console.log('Llamada a un Grafo Hamiltoniano');
            var ham =this.isHamiltoniano()
            return ham
        },

        delAndClear(){
            console.log('Se limpian los datos');
            this.eliminarGrafo();
            this.drawGrafo();
        },     

        drawGrafo(){
            if(process.client){
                console.log('Se dibuja el Grafo del lado del cliente');
                var container= document.getElementById("grafo");
                var data={nodes:this.nodos,
                        edges:this.aristas};
                var options = {
                    height: 520 + 'px',
                };
                var network= new vis.Network(container,data,options);
                var djasd = this.matrizAdyacencia()
            }
        },

        drawArbol(){
            if(process.client){
                console.log('Se dibuja el arbol del lado del cliente');
                var container= document.getElementById("arbol");
                var data={nodes:this.nodos,
                        edges:this.caminoPrim};
                var options = {
                    height: 520 + 'px',
                };
                var network= new vis.Network(container,data,options);
            }
            
        },

        mostrarArbol()
        {
            console.log('Se Muestra el arbol');
            this.showArbol=true;
            this.drawArbol();
        },


        drawGrafoDirigido(){
            if(process.client){
                var container= document.getElementById("grafo");
                var data= {nodes:this.nodos,
                        edges:this.aristas};
                var options ={
                    height: 520 + 'px',
                    edges:{
                        arrows:'to',
                    },
                }
                console.log('Se dibuja el grafo dirigido');
                var network= new vis.Network(container,data,options);
                
            }
        },

        drawGrafoEtiquetadoNoDirigido()
        {
            if(process.client){
                console.log('Se dibuja el grafo etiquetado');
                var container= document.getElementById("grafo");
                var data= {nodes:this.nodos,
                        edges:this.aristas};
                var options={
                    height:520 + 'px',
                };
                var network= new vis.Network(container,data,options);
            }
        },

        createNode()
        {
            console.log('Se Crea un nodo');
            this.create=true;
            this.createAris=false;
        },
        
        createArista(){
            console.log('Se Crea una arista');
            this.createAris=true;
            this.create=false;
        },

        crearNodo(){

            if(this.nodo.id==='')
            {
                alert('Debe ingresar un id.');
                console.log('El nodo se ingresa sin id');
                return;
            }
            for(var i=0; i<this.nodos.length;i++)
            {
                if(this.nodos[i].id==this.nodo.id)
                {
                    console.log('El Nodo ya existe',this.nodo.id);
                    alert('El nodo ya existe. Ingrese otro id.');
                    return;
                }
            }
            this.nodo.label=this.nodo.id;
            this.nodos.push(this.nodo);
            console.log('Se agrega el nodo:', this.nodo.id);
            this.nodo={id:'', label:'',color:'#0BC596'}
            this.drawGrafo();
        },
        
        crearArista(){

            if(this.option===1)
            {

                if(this.arista.from==='' || this.arista.to==='')
                {
                    alert('Debe ingresar los extremos de la arista.');
                    console.log('Se intenta dibujar el grafo sin aristas');
                    return;
                }
                for(var i=0; i<this.aristas.length;i++)
                {
                    if(this.arista.from===this.aristas[i].from && this.arista.to===this.aristas[i].to)
                    {
                        alert('ya existe la arista. Igrese otra');
                        console.log('Ya Existen las aristas');
                        return;
                    }
                }
                this.aristas.push(this.arista);
                console.log('Se crea la arista', this.arista);
                this.arista={from:'',to:'',color:{color:'rgb(0,0,0)'},font:{color:'rgb(255,255,255)'}};
                this.drawGrafo();
            }
            
            if(this.option===2)
            {
                if(this.aristaDirigido.from==='' || this.aristaDirigido.to==='')
                {
                    alert('Debe ingresar los extremos de la arista.');
                    console.log('No se agregan los extremos');
                    return;
                }
                for(var i=0; i<this.aristas.length;i++)
                {
                    if(this.aristaDirigido.from===this.aristas[i].from && this.aristaDirigido.to === this.aristas[i].to)
                    {
                        alert('ya existe la arista. Ingrese otra');
                        console.log('Ya existe la arista');
                        return;
                    }
                }
                this.aristas.push(this.aristaDirigido);
                console.log('Se Agrega la arista:', this.aristaDirigido);
                this.aristaDirigido={from:'', to:'', color:{color:'rgb(0,0,0)'},font:{color:'rgb(255,255,255)'}};
                this.drawGrafoDirigido();
                var ady= this.matrizAdyacenciaDirigido();
            }

            if(this.option===3)
            {
                if(this.aristaEtiquetadaDirigida.from==='' || this.aristaEtiquetadaDirigida.to==='' || this.aristaEtiquetadaDirigida.label==='')
                {
                    alert("extremos de aristas o peso no indicado. Rellene todos los campos antes de continuar");
                    return;
                }
                for(var i=0; i<this.aristas.length;i++)
                {
                    if(this.aristaEtiquetadaDirigida.from===this.aristas[i].from && this.aristaEtiquetadaDirigida.to===this.aristas[i].to)
                    {
                        alert("La arista ya existe. Ingrese otra");
                        return;
                    }
                    
                }
                this.aristas.push(this.aristaEtiquetadaDirigida);
                console.log('Se agerga la arista',this.aristaEtiquetadaDirigida);
                this.aristaEtiquetadaDirigida={from:'', to:'', label:'',color:{color:'rgb(0,0,0)'},font:{color:'rgb(255,255,255)'}};
                this.drawGrafoDirigido();
                var ady= this.matrizAdyacenciaDirigido();
            }

            if(this.option===4)
            {
                if(this.aristaEtiquetada.from==='' || this.aristaEtiquetada.to==='' || this.aristaEtiquetada.label==='')
                {
                    alert("extremos de aristas o peso no indicado. Rellene todos los campos antes de continuar");
                    return;
                }
                for(var i=0; i<this.aristas.length;i++)
                {
                    if(this.aristaEtiquetada.from===this.aristas[i].from && this.aristaEtiquetada.to===this.aristas[i].to)
                    {
                        alert("La arista ya existe. Ingrese otra");
                        return;
                    }
                    
                }
                this.aristas.push(this.aristaEtiquetada);
                console.log('Se agrega la arista', this.aristaEtiquetada);
                this.aristaEtiquetada={from:'', to:'', label:'',color:{color:'rgb(0,0,0)'},font:{color:'rgb(255,255,255)'}};
                this.drawGrafoEtiquetadoNoDirigido();
                var ady=this.matrizAdyacencia();

            }
        },

        mostrarOp1(){
            this.controlanalisis=1;
            this.matrizCaminos();
            this.Adyacencia=this.matrizAdyacencia();
            this.esConexo=this.conexo();
        },

        mostrarOp2(){
            this.controlanalisis=2;
        },

        mostrarOp3(){
            this.euler=this.isEuleriano();
            this.controlanalisis=3;
        },

        mostrarOp4(){
            this.controlanalisis=4;
        },

        mostrarOp5(){
            this.controlanalisis=5;
            this.drawArbol();
        },

        matrizAdyacencia(){
            let matrix=[]; 
            var n = this.nodos.length;
            var e = this.aristas.length;
            for (var i=0; i<n;i++){
                matrix[i]=new Array(n);
            }
            
            for(var i=0; i<n; i++){
                for(var j=0; j<n; j++){
                    matrix[i][j]=0;
                }
            }
            
            for (var i=0; i<e;i++){
                var n1= this.aristas[i].from;
                var n2= this.aristas[i].to;
                matrix[n1-1][n2-1]=1;
                matrix[n2-1][n1-1]=1;
            }
            console.log('Matriz adyacencia',matrix); 
            return matrix;        
        },

        matrizAdyacenciaDirigido()
        {
            let matrix=this.crearMatriz()
            for(var i=0; i<this.nodos.length; i++)
            {
                for(var j=0; j<this.nodos.length;j++)
                {
                    matrix[i][j]=0;
                }
            }
            for(var i=0; i<this.aristas.length;i++){
                var n1=this.aristas[i].from;
                var n2=this.aristas[i].to;
                matrix[n1-1][n2-1]=1;
            }
            console.log('Se imprime la matriz', matrix);
            return matrix;
        },

        conexo(){
            var matriz = this.sumaMat();
            var largo = this.nodos.length;
            for(var i=0;i<largo;i++){
                for(var j=0;j<largo;j++){
                    if(matriz[i][j]===0){
                        console.log('Conexo matriz', false);
                        return false;
                    }
                }
            }
            console.log('Conexo matriz', true);
            return true;
        },

        graficarCircuitoEuleriano(){
            var e=this.eleccion;
            let pasos=[];
            let aux=this.matrizAdyacencia();
            let control=3;
            let indice;
            let largo=this.nodos.length;
            for(var i=0; i<this.nodos.length; i++){
                if(this.nodos[i].id==e){
                    if( i < (this.nodos.length/2) ){
                        control=0;
                    }else{
                        if( i >= (this.nodos.length/2) ){
                            control=1;
                        }
                    }
                    indice=i;
                }
            }

            if(control==3){
                alert("Ingrese Id valido")
                return;
            }else{
                if(control==1){
                    pasos.push(indice+1); 
                    for( indice; indice < this.nodos.length; indice++){
                        for(var j=0; j<this.nodos.length; j++){
                            if(aux[indice][j]==1){
                                aux[indice][j]=2;
                                aux[j][indice]=2;
                                indice=j-1;
                                pasos.push(j+1);
                                j=this.nodo.length+1; 
                            }
                        }
                    }
                }else{
                    pasos.push(indice+1);  
                    for( indice; indice < this.nodos.length; indice++){
                        for(var j=largo-1; j>=0; j--){
                            if(aux[indice][j]==1){
                                aux[indice][j]=2;
                                aux[j][indice]=2;
                                indice=j-1;
                                pasos.push(j+1);
                                j=-1;
                            }
                        }
                    }
                    this.arregloEuleriano=pasos
                }
            }
        },

        isEuleriano(){ 
            if(this.conexo()){
                var grados=0;
                var matriz=this.matrizAdyacencia();
                for(var i=0; i<this.nodos.length; i++){
                    grados=0;
                    for(var j=0; j<this.nodos.length;j++){      
                        if(matriz[i][j]==1){
                            if(i==j && matriz[i][j]==1){
                               grados+=2;
                            }
                            else{
                               grados++;
                            }
                        }
                    }
                    if(grados%2!=0){
                        return false;
                    }
                }               
                return true;
            }
            else{
                return false;
            }
        },

        gradosHam(grados,matrix){
            for(var i = 0; i < this.nodos.length; i++){
                    var cont = 0 
                    for( var j = 0 ; j < this.nodos.length; j++){
                        if(matrix[i][j]==1){
                            cont++;
                        }
                    }
                    grados.push(cont)
                }
            return grados
        },

        isHamiltoniano(){
            
            if(this.conexo()){
                var matrix = this.matrizAdyacencia();
                var grados = [];
                var nodo_inicio = this.eleccion;
                var posicion = nodo_inicio-1;
                var contadorAristas = 0;
                var camino = [];
                var control=0;
                grados=this.gradosHam(grados,matrix)

                while(contadorAristas!=this.nodos.length){
                    camino.push(posicion);
                    grados = []
                    grados=this.gradosHam(grados,matrix)
                    var adyacencia=[];
                    contadorAristas++;
                    for(var j=0; j<this.nodos.length; j++){
                        if(this.esta(camino, j)==false && grados[j]>1){
                            if( matrix[posicion][j] == 1 && j != nodo_inicio-1){
                                adyacencia.push(j);
                            }
                        }
                    }
                    
                    if(adyacencia.length==0 && contadorAristas!=this.nodos.length){
                        return false
                    }
                    var menor=adyacencia[0];
                    var aux=0;
                    
                    for(var k=0; k<adyacencia.length; k++){
                        if( grados[adyacencia[aux]] > grados[adyacencia[k]] && k != nodo_inicio-1 ){
                            aux=k;
                            menor=adyacencia[k];
                        }
                        
                    }
                    
                    if(control!=0){
                        for(var n=0; n<this.nodos.length; n++){
                            matrix[posicion][n]=0;
                            matrix[n][posicion]=0;
                        }
                    }
                    else{
                        control=1;
                    }
                    posicion=menor;
                    grados[posicion]=0  
                    
                }
                if(camino.length==this.nodos.length){
                    camino.push(parseInt(nodo_inicio-1));
                }else{
                    return false;
                }
                this.hamilton = camino;
                return true
            }
            else{
                return false;
            }
        },

        arreglomas1(arreglo){
            for(var i=0 ; i< arreglo.length; i++){
                arreglo[i]++
            }
            return arreglo
        },

        esta(camino, num){
            for(var i=0; i<camino.length-1; i++){
                
                if(num==camino[i]){
                    
                    return true;
                }
            }
            return false;
        },

        matrizCostos(){
            let matrix=this.crearMatriz()
            for(var i=0; i<this.nodos.length; i++)
            {
                for(var j=0; j<this.nodos.length;j++)
                {
                    matrix[i][j]=null;
                }
            }
            for(var i=0; i<this.aristas.length;i++)
            {
                var n1=this.aristas[i].from;
                var n2=this.aristas[i].to;
                matrix[n1-1][n2-1]=parseInt(this.aristas[i].label);
                
            }
            
            return matrix;
        },

        buscarNodoD(idNodo,d){
            for(let i=0 ;i<d.length; i++){
                if(d[i][0]==idNodo){
                    return i;
                }
            }
        },

        existe(){
            for(var i=0; i<this.nodos.length;i++)
            {
                if(this.nodos[i].id===this.inicio)
                {
                    return true;
                }
            }
            return false;
        },
        caminoCorto(){
           this.getDijkstra=[];
           if(!this.existe())
           {
               alert("id Inválido. Reintente nuevamente.");
               return;
           }
           if(this.conexo()){
               
               var matrix = this.matrizCostos()
               var maximo=0;
               let dijs = [];
               let visitados = [];
               for(let i=0;i<this.nodos.length;i++){
                   for(let j=0;j<this.nodos.length;j++){
                       if(matrix[i][j]!=null){
                           maximo = maximo + matrix[i][j]
                       }
                   }
               }    
                for(let k=0;k<this.nodos.length;k++){
                    
                    let aux=new Array(4);
                    aux[0]= this.nodos[k].id;
                    aux[1]= maximo;
                    aux[2]= null;
                    aux[3]= 0;
                    dijs.push(aux);
                }
                let posIn = this.buscarNodoD(this.inicio,dijs);
                dijs[posIn][1]=0
                dijs[posIn][2]=this.inicio
                
                while(visitados.length<dijs.length){
                    let menor = maximo 
                    let posicionMenor = -1
                    for(let d=0 ;d<dijs.length;d++){
                        if(dijs[d][3]!=1 && dijs[d][1]<=menor){
                            menor = dijs[d][1]
                            posicionMenor = d;
                        }

                    }
                    dijs[posicionMenor][3] = 1;
                    visitados.push(dijs[posicionMenor][0]);
                    if(visitados.length<dijs.length && menor!=maximo){
                        for(let f=0;f<this.nodos.length;f++){
                            if(matrix[posicionMenor][f]!=null && dijs[f][3]!=1){
                                let suma = dijs[posicionMenor][1] + matrix[posicionMenor][f];
                                if(suma < dijs[f][1]){
                                    dijs[f][1] = suma
                                    dijs[f][2] = dijs[posicionMenor][0]
                                }
                            }
                        }       

                    }
                    this.dijkstra=dijs;
                    
                }
            }
            else
            {
                return false;
            }
            this.caminosDijkstra()
            
        },

        caminosDijkstra()
        {
            var caminos=[];
            var  pesos=[]
            for(var i=0; i<this.dijkstra.length;i++)
            {   
                var  camino=[]
                pesos.push(this.dijkstra[i][1])
                if(this.dijkstra[i][0]!=this.inicio)
                {
                    var nodo_actual=i;
                    if(this.dijkstra[nodo_actual][2]!=null)
                    {
                        while(this.dijkstra[nodo_actual][0]!=this.inicio)
                        {
                            camino.push(this.dijkstra[nodo_actual][0])
                            nodo_actual=this.buscarNodoD(this.dijkstra[nodo_actual][2],this.dijkstra)
                        }

                    }
                    else
                    {
                        camino.push(null);
                        
                    }
                }
                else{
                    camino.push(this.inicio)
                }
                caminos.push(camino);
            }
            console.log('Caminos:', caminos);
            console.log('Pesos', pesos);
            this.mostrarDijkstra(caminos,pesos)
        },

        mostrarDijkstra(caminos,pesos)
        {
            for(var i=0; i<caminos.length;i++)
            {
                if(caminos[i][0]==this.inicio){
                }
                else{
                    if(caminos[i][0]==null)
                    {
                    }
                    else{
                        var aux=caminos[i].reverse();
                        this.getDijkstra.push(aux);
                    }
                }
            }
        },


        verificarVisitados(noVisitados,visitados,j){
            for(var i=0; i<this.nodos.length;i++){
                if(noVisitados[i].id==j){
                    visitados.push(noVisitados[i])
                    
                }
            }
        },

        arrayControl(largo){
            var array=[];
            for(var i=0; i<largo; i++){
                array.push(0);
            }
            return array;
        },

        buscarPos(vertices, e){
            for(var i=0; i<vertices.length; i++){
                if(vertices[i]==e){
                    return i;
                }
            }
        },

        prim(){
            if(this.conexo()){
                var agm=[];
                var vertices= [];
                this.nodos.forEach(element => {
                    vertices.push(element.id);
                });
                var control=this.arrayControl(this.nodos.length);
                let aristas1= this.$_.sortBy(this.aristas, function(indice){return parseInt(indice.label);});
                aristas1.forEach(element => {
                    console.log(element.label, element.from, element.to)
                });
                control[0]=1;
               
                while(agm.length<this.nodos.length-1){
                    for(var i=0; i<aristas1.length; i++){
                        if(control[this.buscarPos(vertices, aristas1[i].from)] != control[this.buscarPos(vertices, aristas1[i].to)]){
                            agm.push(aristas1[i]);
                            control[this.buscarPos(vertices, aristas1[i].from)]=1;
                            control[this.buscarPos(vertices, aristas1[i].to)]=1;
                            i=aristas1.length+3;
                        }
                    }
                }
                agm.forEach(element => {
                    console.log('from:',element.from);
                    console.log('to',element.to);
                });
                this.caminoPrim=agm;
                return true;
            }else{
                return false;
            }
            
        },

        flujoMaximo(inicio, final){
            var matriz_caminos=[], camino=[];
            var visitados=[];
            var matrizAdy=this.matrizAdyacenciaDirigido();
            this.buscarCaminos(matriz_caminos, camino, matrizAdy, inicio-1, final, visitados);

            var menor=1;
            var rama;
            var camino;
            var acumulado=0;
            var inicio=1;
            var fin=7;
            if(this.camino(inicio,destino))
            {
                camino=this.caminoflujo();
            }
            for(var i=0; i<vertices.length; i++){
                if(vertices[i]==e){
                    return true;
                }
            }
            return false;
        },

        buscarCaminos(matriz, array, adyacencia, inicio, fin, visitados){
            for(let i=0; i<this.nodos.length; i++){
                if(adyacencia[inicio][i]==1){
                    if(inicio!=fin && this.existe(visitados, i)==false){
                        array.push(this.nodos[i].id);
                        adyacencia[inicio][i]=0;
                        visitados.push(inicio);
                        matriz.push(this.buscarCaminos(matriz, array, adyacencia, i, fin, visitados));
                    }else{
                        if(inicio==fin){
                            array.push(this.nodos[i].id);
                            return array;
                        }
                    }
                }
            }
        },

        multiplicarMatriz(matrizA,matrizB)
        {
            let res=[];
            var sum=0;
            
            for(var i=0; i<matrizA.length;i++)
            {
                res[i]= new Array(matrizA.length);
            }
            
            for(var a=0;a<matrizB.length;a++)
            {
                for(var i=0; i<matrizA.length;i++)
                {
                    sum=0;
                    for(var j=0; j<matrizA.length;j++)
                    {
                        sum+= matrizA[i][j]*matrizB[j][a];
                    }
                    res[i][a]=sum;
                }
            }
            return res;	
        },

        potencia(matriz, largo )
        {
            var sum=0;
            var aux=matriz;
            var res;
            for(var i=1; i < largo-1 ;i++)
            {
                res=this.multiplicarMatriz(matriz,aux);
                aux=res;
                
            }    
            return res;      
        },

        matrizCaminos()
        {
            this.matrixCaminos=this.sumaMat();
        },

        sumaMat(){
            var matrizId = this.matrizIdentidad();
            var matrizAd = this.matrizAdyacencia();
            var largo = this.nodos.length;
            let aux = this.crearMatriz();
            let sumPot;
            
            for(var i=0 ; i<largo ; i++ ){
                for(var j=0 ; j<largo ;j++){
                    aux[i][j] =  matrizId[i][j] + matrizAd[i][j];
                }
            }
            for(var i=largo;i>2;i--)
            {
                sumPot=this.potencia(matrizAd,i);
                for(var j=0; j<this.nodos.length;j++)
                {
                    for(var k=0;k<this.nodos.length;k++)
                    {
                        aux[j][k]=aux[j][k]+sumPot[j][k];
                    }
                }
            }

            return aux;
        },

        crearMatriz(){
            var res = [];
            for(var i=0; i<this.nodos.length;i++)
            {
                res[i]= new Array(this.nodos.length);
            }
            return res;
        },
        
        matrizIdentidad(){
            let matriZIdentidad=[];
            var largo = this.nodos.length;
            for(var i=0; i < largo; i++)
            {
                matriZIdentidad[i] = new Array(largo);    
            }
            
            for(var i=0; i < largo ; i++)
            {
                for(var j=0; j < largo ; j++)
                {
                    if(i===j)
                    {
                        matriZIdentidad[i][j]=1;
                    }
                    else{
                        matriZIdentidad[i][j]=0;
                    }
                }
            }
        return matriZIdentidad;
        },
        
        eliminarGrafo(){
            this.nodos=[];
            this.aristas=[];
            console.log('Elimina los nodos',this.nodos);
            console.log('Elimina las aristas', this.aristas);
        },

    },

}
</script>