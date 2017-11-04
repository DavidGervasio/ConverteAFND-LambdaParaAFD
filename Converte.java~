
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.io.InputStreamReader;


public class Converte {

	public static void main(String[] args) throws IOException {
		
		
		String ArquivoDeEntrada = args[0];
		String ArquivoDeSaida = args[1];
			
		// TODO Auto-generated method stub

		/*
		 *Maquina de entrada deve estar contido em um arquivo 
		 *e obdecer a este padrão obs: Sem tabulação;
		 
		 (
		 {q0,q1,q2},
		 {a,b,c},
	    	 {
		 (q0,a)->{q0,q1,q2},
		 (q1,b)->{q1},
		 (q2,c)->{q2},
		 (q2,.)->{q1}
		 },
		 q0,
		 {q1}
		 )
		 
		 
		 *Obs: para fins praticos a variavel " maximoDeEstadoAFD " foi definida em 30 
		 *sendo que teoricamnte ela deveria ser definda como "2^quantidade de estados" 
		 */
		
		
		FileReader arq = new FileReader(ArquivoDeEntrada);
		BufferedReader lerArq = new BufferedReader(arq);
		
		
	    int quantidadeEstados = 0; 
	    int tamanhoDoAlfabeto = 0;
	    int [][][] tabelaAFNDLambda;
		int [][][] tabelaAFND;
		int [][][] tabelaAFD;
		/*Numero de linha representa os estados
		Numero de colunas representa alfabeto
		ex:
		q1 = 1 , q2 = 2... 
		a=1, b=2 ...
		*/
			
		String readLine = lerArq.readLine(); // Ler linha 1 e descartar '('
		readLine = lerArq.readLine(); // Ler linha 2// linha do conjunto de estados {q1,q2,q3..},
				
		String[] removeLinhaBranca = readLine.split("}");//Separar conjunto
		char [] vetorChar = removeLinhaBranca[0].toCharArray();//Converter  String em um vetor de char
	
		for(int i=0; i<vetorChar.length; i++)//Contar quantos estados estão no conjunto
				if(vetorChar[i] == 'q')
					quantidadeEstados++;
	
	   int tamanhoMaxDosConjuntos =  quantidadeEstados + 1; 
	   /*Garante que o ultimo elemento do conjunto 
	   seja invalido(999) para garantir condições de parada
	   ex:
	   while( tabelaAFNDLambda[ linha ][ coluna ][ elementoDoConjunto ] != 999  )
	   */
	    
	    readLine = lerArq.readLine(); // Ler linha 3 // conjunto de alfabeto ex: {a, b, c}
		removeLinhaBranca = readLine.split(" ");//Separar conjunto
		vetorChar = removeLinhaBranca[0].toCharArray();//Converter  String em um vetor de char
		
		for(int i=0; i<vetorChar.length; i++)//Contar quantos simbolos estão no conjunto
				if(vetorChar[i] == ',')
						
		
		tamanhoDoAlfabeto++;//Correção sempre uma virgula mais ex{a,b} 2 simbolos 1 virgula//?mas ja temos tres virgulas nesta linha
		
		int colunaLambda =  tamanhoDoAlfabeto;
		
		int quantidadeDeColunasTabelaAFNDLambda =  tamanhoDoAlfabeto + 2;//coluana lambda e fecho lambda 
		int colunaFechoLambda = colunaLambda + 1;
		
		tabelaAFNDLambda = new int [tamanhoMaxDosConjuntos][quantidadeDeColunasTabelaAFNDLambda][tamanhoMaxDosConjuntos];//O tamanho max dos cunjuntos(terceiro vetor da tabela) é o número de estados
							
		for(int i=0; i< tamanhoMaxDosConjuntos; i++){//Preencher tabela
				for(int j=0; j< quantidadeDeColunasTabelaAFNDLambda; j++){
						for(int l=0; l< tamanhoMaxDosConjuntos; l++){
								tabelaAFNDLambda[i][j][l] = 999;
						}	
										
				}
							
		}
							
		
		readLine = lerArq.readLine(); // Ler linha 4 e descartar 
		readLine = lerArq.readLine(); // Ler linha 5 e descartar 
		removeLinhaBranca = readLine.split(" ");//Separar conjunto
		vetorChar = removeLinhaBranca[0].toCharArray();//Converter  String em um vetor de char
	
		
		while(vetorChar[0] != '}'  ){//Loop ate o fim do conjunto de transições
			
				int posConjunto = 0;//Conta a posição onde serar inserido os estados
				int i = 2; // 2 pois pula '(q'
				String StringAux = String.valueOf(vetorChar[i]);
				i++;//Para no numero
				while( vetorChar[i] != ','){//Concatena o numero
						StringAux =	StringAux   +  String.valueOf( vetorChar[i]) ;  
						i++;
				}
				i++;// Ler um a , b ...
				int  estadoLinha = Integer.parseInt( StringAux );
		
				int caracterColuna =  (int)vetorChar[i];//Equivalencia a = 0 b = 1 ...
			
			
			
				if(caracterColuna == '.'){//Coluna de transição lambda é a ultima 
				/* Convert . == lambda coluna lambde é sempre a ultima logo
				 * "colunaLambda + 48 refere-se a um numero da tabela da tabela ascii
				 * Ex: 50(ascii)  = 2(coluna)	
				 * Obs: O metodo "getNumericValue" recebe um numero decimal da tabela ascii
				 */
						caracterColuna = colunaLambda + 48;
			
				}else{
						caracterColuna = caracterColuna - 49 ;//Converte letra para numero ex: a = 0, b = 1 ...//Referente a coluna
				}
				i+=5;// Pular ")->{q" 
				posConjunto = 0;
				
				do{//Conjunto dessa transição
				
						i++;
						StringAux = String.valueOf(vetorChar[i]);
						i++;
						while( vetorChar[i] != ',' && vetorChar[i] != '}'){//Concatena o numero
								StringAux =	StringAux  + String.valueOf( vetorChar[i]) ;  
								i++;	
						}
						if(i < vetorChar.length-1)//Proteção para i não ultrapassar o tamanho do vetorChar
								i++;
					
						tabelaAFNDLambda[  estadoLinha  ][ Character.getNumericValue(caracterColuna) ][ posConjunto ] = Integer.parseInt( StringAux )  ;
						posConjunto++;	
			
				}while(vetorChar[i] == 'q');//Marca o fim do conjunto dessa transição
			
				readLine = lerArq.readLine(); 
				removeLinhaBranca = readLine.split(" ");//Separar conjunto
				vetorChar = removeLinhaBranca[0].toCharArray();//Converter  String em um vetor de char
		
		}//Fim do loop da laitura de todas as transiçoes do conjunto de transiçoes
								
		
		for(int estado = 0; estado < quantidadeEstados; estado++)//Para cada estado(linha da tabela) forma seu Fecho Lambda
				fecholambdaRecursiva(tabelaAFNDLambda, colunaLambda, colunaFechoLambda, estado, estado);
		
	
		tabelaAFND = new int [ tamanhoMaxDosConjuntos ][  tamanhoDoAlfabeto ][ tamanhoMaxDosConjuntos ];	//Montar tabela afnd
		
		for(int i=0; i< tamanhoMaxDosConjuntos; i++){//Preencher tabela
			for(int j=0; j<  tamanhoDoAlfabeto; j++){
					for(int l=0; l< tamanhoMaxDosConjuntos; l++){
							tabelaAFND[i][j][l] = 999;
					}	
			}
		}
		

		
		
				for(int linha = 0; linha < quantidadeEstados;  linha ++ ){
						/*Este conjunto de instrução realiza a montagem da tabaela AFND.
						 *É dividido e duas partes:
						 *
						 *1 Parte:
						 *	 Realiza a inserção que eu chamo de inserção em "L".
						 *	 Para cada elemento(estado) do conjunto pertencente 
						 *	 tabelaAFNDLambda[linha][coluna][...] va ate ao seu Conjunto Fecholambda 
						 *	 e insira na tabelaAFND[linha][coluna][...]
						 * 
						 */
					
						for(int coluna = 0; coluna < tamanhoDoAlfabeto; coluna++){
								
								int elementoDoConjunto = 0;
								
								while( tabelaAFNDLambda[ linha ][ coluna ][ elementoDoConjunto ] != 999  ) {//Loop em todos os elementos do conjunto 
									
									if( verificarExistenciaDoElementoNoCojunto( tabelaAFND, linha, coluna, tabelaAFNDLambda[ linha ][ coluna ][ elementoDoConjunto] ) == false )
												inserirOrdenado( tabelaAFND, linha, coluna, tabelaAFNDLambda[ linha ][ coluna ][ elementoDoConjunto] );
										/*Erro em estrutura de if sem chaves "{}":  Apos o cabeçãlho do if "if(...)" não si deve utilizar ";"*/
										int elementoDoFechoLambda = 0;
								
										while( tabelaAFNDLambda[      tabelaAFNDLambda[ linha ][ coluna ][ elementoDoConjunto] /*  Linha do elemento(estado) que foi inserido*/     ][ colunaFechoLambda ][ elementoDoFechoLambda] != 999) {//Até o ultimo elemento valido
												if( verificarExistenciaDoElementoNoCojunto( tabelaAFND, linha, coluna, tabelaAFNDLambda[   tabelaAFNDLambda[ linha ][ coluna ][ elementoDoConjunto ]   ][ colunaFechoLambda ][ elementoDoFechoLambda ] ) == false )
														inserirOrdenado( tabelaAFND, linha, coluna, tabelaAFNDLambda[      tabelaAFNDLambda[ linha ][ coluna ][ elementoDoConjunto]     ][ colunaFechoLambda ][ elementoDoFechoLambda] );
											
										elementoDoFechoLambda++;	
								}
								
										elementoDoConjunto++;
							
								
								}//Fim do while // Fim da inserção em "L"
								
								
								
								
								
								
								
								int elementoDoConjuntoFechoLambda = 0;
								while( tabelaAFNDLambda[ linha ][ colunaFechoLambda ][ elementoDoConjuntoFechoLambda ] != 999  ) {//Loop em todos os elementos do conjunto fecho lambda 
										
										/*2 Parte:
										 * 	Realiza a inserção que eu chamo de "Z" 
										 *  Para cada elemento pertecente tabelaAFNDLambda[ linha ][ colunaFechoLambda ][ elementoDoConjuntoFechoLambda ] (conjunto fecho lambda da linha atual)
										 *  va ate sua posição na tabela tabelaAFNDLambda e verifique e exite elemento para a transição atual(ou seja a coluna que é igual ao simbolo)
										 *  si exite insere esse elemento (caso nao tenha sido inserido ainda) na tabela tabelaAFND[linha][coluna][...]
										 * 	em seguida realizar inserção em "L"  desse elemento 
										 * 
										 * 
										 * */	
									
									
									
									
										elementoDoConjunto = 0;
											while( tabelaAFNDLambda[  /*Elemento do fecho lambda*/  tabelaAFNDLambda[ linha ][ colunaFechoLambda ][ elementoDoConjuntoFechoLambda ]   ][ coluna ][ elementoDoConjunto ] != 999  ) {//Loop em todos os elementos do conjunto 
													if( verificarExistenciaDoElementoNoCojunto( tabelaAFND, linha, coluna, tabelaAFNDLambda[       tabelaAFNDLambda[ linha ][ colunaFechoLambda ][ elementoDoConjuntoFechoLambda ]      ][ coluna ][ elementoDoConjunto] ) == false )
															inserirOrdenado( tabelaAFND, linha, coluna,  tabelaAFNDLambda[        tabelaAFNDLambda[ linha ][ colunaFechoLambda ][ elementoDoConjuntoFechoLambda ]       ][ coluna ][ elementoDoConjunto] );
															//Erro em estrutura de if sem chaves "{}":  Apos o cabeção do if "if(...)" não si deve utilizar ";"
															int elementoDoFechoLambda = 0;
								
															while( tabelaAFNDLambda[     tabelaAFNDLambda[        tabelaAFNDLambda[ linha ][colunaFechoLambda ][ elementoDoConjuntoFechoLambda ]       ][ coluna ][ elementoDoConjunto]     ][ colunaFechoLambda ][ elementoDoFechoLambda] != 999) {//Até o ultimo elemento valido
																	if( verificarExistenciaDoElementoNoCojunto( tabelaAFND, linha, coluna, tabelaAFNDLambda[  tabelaAFNDLambda[        tabelaAFNDLambda[ linha ][  colunaFechoLambda ][ elementoDoConjuntoFechoLambda ]       ][ coluna ][ elementoDoConjunto]   ][ colunaFechoLambda ][ elementoDoFechoLambda ] ) == false )
																			inserirOrdenado( tabelaAFND, linha, coluna,  tabelaAFNDLambda[     tabelaAFNDLambda[        tabelaAFNDLambda[ linha ][ colunaFechoLambda ][ elementoDoConjuntoFechoLambda ]       ][ coluna ][ elementoDoConjunto]     ][ colunaFechoLambda ][ elementoDoFechoLambda] );
											
																	elementoDoFechoLambda++;	
															}
								
															elementoDoConjunto++;
							
								
											}//Fim do while 
						
										elementoDoConjuntoFechoLambda++;
								
								}//Fim do  while da segunda parte
						
						}
				}
		
	
		
		
		
		/*Montagem da tabela AFD que contem "TamanhoDoAlfabeto + 1" colunas(coluna 0) onde 
		 *a primeira coluna sera inserido os novos conjuntos.
 	         *
		 *Geração de conjunto por demanda
		 *
		 *Obs: Si o AFND tiver 'n' estados então o AFD pode ter 
		 *no maximo 2 elevado n estados
		 **/
		
		 
		 int maximoDeEstadoAFD = 30;// (int) (Math.pow(2,quantidadeEstados) + 1) ;
		
	
		tabelaAFD = new int [  maximoDeEstadoAFD  ][  tamanhoDoAlfabeto + 1 ][ tamanhoMaxDosConjuntos ];// "TamanhoDoAlfabeto + 1" 	Pois temos um nova coluna de conjunto "coluna 0" 
		
		for(int i=0; i< maximoDeEstadoAFD; i++){
			for(int j=0; j<  tamanhoDoAlfabeto + 1; j++){
					for(int l=0; l< tamanhoMaxDosConjuntos; l++){
							tabelaAFD[i][j][l] = 999;
					}	
			}
		}
		
		int linha = 0; 
		
		tabelaAFD[0][0] =  tabelaAFNDLambda[ 0 ][ colunaFechoLambda  ]; //Define o primeiro da tabela AFD como o conjunto fecho lambda d q0
	
	
		
		while( tabelaAFD[ linha ][ 0 ][ 0 ] != 999  ) {
			/*Si o primeiro elemento do conjunto for 999 
			 * ele esta vazio
			 * Em outras palavras marca ate onde existe conjuto
			 * na coluna 0(primeira coluna)	
			Loop em toda coluna 0*/
			
			
			
			
			
			for(int coluna = 1; coluna < tamanhoDoAlfabeto +1; coluna++){//Coluna inicia no 1 pois a coluna 0 pertence aos novas estados que serão inseridos em outra parte
					
					int elementoDoNovoEstado = 0;
					
					while( tabelaAFD[ linha ][ 0 ][elementoDoNovoEstado] != 999  ) {//Loop em todos os elementos do conjunto 
						/* Para cada elemento do conjunto(Novo estado na coluna 0)
						 * na tabela AFD vai na tabela AFND e insere o conjuto
						 * da sua transiçao de acordo com a entrada 
						 * (letra do alfabeto coluna )  */
						
						
						
							int elementoDaTabelaAFND = 0;
					
							while( tabelaAFND[/*linha*/  tabelaAFD[ linha ][ 0 ][ elementoDoNovoEstado ]     ][  coluna -1/*-1 Correção entre tabelas*/  ][ elementoDaTabelaAFND ] != 999) {//Até o ultimo elemento valido
									if( verificarExistenciaDoElementoNoCojunto( tabelaAFD, linha, coluna, tabelaAFND[/*linha*/  tabelaAFD[ linha ][ 0 ][ elementoDoNovoEstado ]     ][ coluna -1 ][ elementoDaTabelaAFND ] ) == false )
											inserirOrdenado( tabelaAFD, linha, coluna, tabelaAFND[/*linha*/  tabelaAFD[ linha ][ 0 ][ elementoDoNovoEstado ]     ][ coluna -1 ][ elementoDaTabelaAFND ] );
									
									elementoDaTabelaAFND++;	
					}
					
							elementoDoNovoEstado++;
				
					
					
							
					
					
					}//Fim do while
					
					
					/*Verificar si o cojunto ja foi inserido
					 *na coluna '0' ou seja si é um novo conjunto
					 *Si for um novo conjunto então inserir
					 */
		
					Boolean conjutoInserido = false;
					
					for(int i = 0; i < maximoDeEstadoAFD; i ++){
							if(  comparaDoisConjunto( tabelaAFD[i][0], tabelaAFD[linha][coluna]  )){
									conjutoInserido=  true;
							}
					}
					
					if( conjutoInserido == false){
			
							//Procurar  o fim da coluna para inserir
							int fimColuna = 0;
						
							while( tabelaAFD[ fimColuna ][ 0 ][ 0 ] !=  999){
									fimColuna++;
							}
							//Inserir Novo Estado 
							tabelaAFD[ fimColuna ][ 0 ] = tabelaAFD[linha][coluna];
					
					}
			
			
			}//Fim Do for
		linha++;
		

		
		
		
		}
		
				
		
		
		/*Escrever arquivo com resultados obtidos 
		  Processo é feito para cada tabela 
		  utilizando um unico arquivo para salvar a 
	'	  informação.
		  Cada tabela e montada linha a linha
	

		*/
		BufferedWriter buffWrite = new BufferedWriter(new FileWriter(ArquivoDeSaida));
	
		//Obs: Cada inserção na linha do aquivo deve contar 5 unidades ex: "....." 
		String espaco =  "   "; 
		for(int i=1; i< quantidadeEstados; i++)//Concatenar espaço em branco "q0         {....}"
				espaco += "   ";
		
		
		buffWrite.write ("TABELA AFND-LAMBDA");
		buffWrite.append("\n");
		/*  Salvando tabela AFND LAMBDA no arquivo	
		 * */
	
		StringBuilder strBuilderCabecalho = new StringBuilder();// Forma cabeçalho da tabela ex: "&            a              b             c         lamb"
		
		strBuilderCabecalho.append("& "+espaco);
		
		for(int i=0 ; i< tamanhoDoAlfabeto; i++){//Concatenar simbolos primeira linha (cabeçalho) da tabela 
				char aux = (char)(i+97);
				String string = aux + espaco;
				strBuilderCabecalho.append(string);
		}

		strBuilderCabecalho.append("L"+espaco);
		
		buffWrite.write (strBuilderCabecalho.toString(),0,strBuilderCabecalho.length());//salvando cabeçalho no arquivo
		buffWrite.append("\n");
		
		
		for(int i=0; i< quantidadeEstados; i++){//Linha(estado)
				
				StringBuilder strBuilderLinha = new StringBuilder();
				strBuilderLinha.append("q"+i+espaco);
				
				for(int j=0; j< quantidadeDeColunasTabelaAFNDLambda - 1; j++){//Coluna(Simbolo) -1 Para nao salva linha fecho lambda no arquivo
						for(int l=0; l< quantidadeEstados; l++){//Elemento do conjunto
								
								if(tabelaAFNDLambda[i][j][l] == 999){
									
										if(l== 0){//Primeiro elemento do conjunto for vazio insera "0"(simbolo de conjuto vazio
								
												strBuilderLinha.append(0+"   ");
								
										}else{
										
												strBuilderLinha.append("   ");
										}
							
							
								}else{
									
										if(l== 0)//Si for o primeiro elemento do conjunto e conjunto nao for vazio insira { antes
												strBuilderLinha.append('{');
									
										//Si for o ultimo elemento do conjunto nao inserir virgula
										if(tabelaAFNDLambda[i][j][l+1] == 999){
												strBuilderLinha.append("q"+tabelaAFNDLambda[i][j][l]+"}");
										}else{
												strBuilderLinha.append("q"+tabelaAFNDLambda[i][j][l]+",");
										}
							
								}
						}
				}
	
			buffWrite.write (strBuilderLinha.toString(),0,strBuilderLinha.length());
			buffWrite.append("\n");
	 }
		

		
		buffWrite.append("\n");
		buffWrite.append("\n");
		buffWrite.write ("TABELA AFND");
		buffWrite.append("\n");
		
		
		/*  Salvando tabela AFND  no arquivo	
		 * */
	
		StringBuilder strBuilderCabecalhoAFND = new StringBuilder();// Forma cabeçalho da tabela ex: "&            a              b             c         lamb"
		
		strBuilderCabecalhoAFND.append("& "+espaco);
		
		for(int i=0 ; i< tamanhoDoAlfabeto; i++){//Concatenar simbolos primeira linha (cabeçalho) da tabela 
				char aux = (char)(i+97);
				String string = aux + espaco;
				strBuilderCabecalhoAFND.append(string);
		}
		
		buffWrite.write (strBuilderCabecalhoAFND.toString(),0,strBuilderCabecalhoAFND.length());//salvando cabeçalho no arquivo
		buffWrite.append("\n");
		
		for(int i=0; i< quantidadeEstados; i++){//Linha(estado)
				
				StringBuilder strBuilderLinha = new StringBuilder();
				strBuilderLinha.append("q"+i+espaco);
				
				for(int j=0; j< tamanhoDoAlfabeto; j++){//Coluna(Simbolo) -1 Para nao salva linha fecho lambda no arquivo
						for(int l=0; l< quantidadeEstados; l++){//Elemento do conjunto
								
								if(tabelaAFND[i][j][l] == 999){
									
										if(l== 0){//Primeiro elemento do conjunto for vazio insera "0"(simbolo de conjuto vazio
								
												strBuilderLinha.append(0+"   ");
								
										}else{
										
												strBuilderLinha.append("   ");
										}
							
							
								}else{
									
										if(l== 0)//Si for o primeiro elemento do conjunto e conjunto nao for vazio insira { antes
												strBuilderLinha.append('{');
									
										//Si for o ultimo elemento do conjunto nao inserir virgula
										if(tabelaAFND[i][j][l+1] == 999){
												strBuilderLinha.append("q"+tabelaAFND[i][j][l]+"}");
										}else{
												strBuilderLinha.append("q"+tabelaAFND[i][j][l]+",");
										}
							
								}
						}
				}
	
			buffWrite.write (strBuilderLinha.toString(),0,strBuilderLinha.length());
			buffWrite.append("\n");
	 }
		
		
		
		
		
		buffWrite.append("\n");
		buffWrite.append("\n");
		buffWrite.write ("TABELA AFD");
		buffWrite.append("\n");
		
		
		
		
		/*  Savando tabela AFD  no arquivo	
		 * */
	
		StringBuilder strBuilderCabecalhoAFD = new StringBuilder();// Forma cabeçalho da tabela ex: "&            a              b             c         lamb"
		
		strBuilderCabecalhoAFD.append("& "+espaco);
		
		for(int i=0 ; i< tamanhoDoAlfabeto; i++){//Concatenar simbolos primeira linha (cabeçalho) da tabela 
				char aux = (char)(i+97);
				String string = aux + espaco;
				strBuilderCabecalhoAFD.append(string);
		}
		
		buffWrite.write (strBuilderCabecalhoAFD.toString(),0,strBuilderCabecalhoAFD.length());//salvando cabeçalho no arquivo
		buffWrite.append("\n");
		
		for(int i=0; i< maximoDeEstadoAFD; i++){//Linha(estado)
				
				StringBuilder strBuilderLinha = new StringBuilder();
				
				
				for(int j=0; j< tamanhoDoAlfabeto + 1; j++){//Coluna(Simbolo) -1 Para nao salva linha fecho lambda no arquivo
						for(int l=0; l< quantidadeEstados; l++){//Elemento do conjunto
								
								if(tabelaAFD[i][j][l] == 999){
									
										if(l== 0 ){ //Si o conjunto for vazio 
											
												strBuilderLinha.append('-'+"   ");
								
										}else{
										
												strBuilderLinha.append("   ");
										}
								}else{
										if(l== 0)//Si for o primeiro elemento do conjunto e conjunto nao for vazio insira { antes
												strBuilderLinha.append('<');
									
										//Si for o ultimo elemento do conjunto nao inserir virgula
										if(tabelaAFD[i][j][l+1] == 999){
												strBuilderLinha.append("q"+tabelaAFD[i][j][l]+">");
										}else{
												strBuilderLinha.append("q"+tabelaAFD[i][j][l]+",");
										}
							
								}
						}
				}
				if(tabelaAFD[i][0][0] != 999){//Si a linha represetar um conjuto salve
						buffWrite.write (strBuilderLinha.toString(),0,strBuilderLinha.length());
						buffWrite.append("\n");
				}
		
		}		
		
		
		buffWrite.close();
		
		//buffWrite.append("\n");
		
		
		//ler o restante da maquina
	

	}//Fim do main

	
	
	public static Boolean comparaDoisConjunto(int[] conjunto1, int [] conjunto2  ){
			/*Verifica si dois conjuntos são iguais 
			 *
			 *Retorna "false" se os dois  conjuntos forem diferentes 
			 *
			 *Bloco e dividido em duas partes 
			 *1 verifica si os dois conjunto possuem tamanhos iguais
			 *2 Verifica elemento a elemento si são iguais 
			 *
			 *Obs: Vetores(Conjuntos) devem estar ordenados
			 * */
				
			Boolean igual = true;
			int i = 0, TamanhoConjunto1 = 0, TamanhoConjunto2 = 0;
			
			while (conjunto1[i] != 999){
					TamanhoConjunto1 ++;
			i++;
			}
				
			i = 0; 
			while (conjunto2[i] != 999){
					TamanhoConjunto2 ++;
			i++;
			}
					
			if( TamanhoConjunto1 ==  TamanhoConjunto2 ){
					i=0;
					while(i < TamanhoConjunto1){
							if( conjunto1[i] != conjunto2[i])
									igual = false; 
					
					i++;
					}					
			}else{	
					igual = false;
			}	
				
		return igual;
	
	}//Fim comparaDoisConjunto

	
	
	public static Boolean verificarExistenciaDoElementoNoCojunto(int[][][] tabelaEntrada,int Linha, int coluna, int  elemento){
			/* Verifica si cunjunto ja possui o elemento que se deseja inserir 
			 * Si o elemento não existe no conjunto retorna false
			 */		
		
			int [][][] tabela = tabelaEntrada;
			Boolean achou = false;
		
			for(int i = 0; i < tabela[Linha][coluna].length; i++)
					if( tabela[Linha][coluna][i] == elemento)
							achou = true;
			return achou;
	}
	
	
	
	
	public static void inserirOrdenado(int[][][] tabelaEntrada, int estadoDonoDaLinha, int coluna, int  elemento){

		int [][][] tabela = tabelaEntrada;
		int posDeslocar = 0, j = 0;
		Boolean inserir = false;
		
		while(inserir != true){//Inserir no lugar do primeiro maior elemento encontrado
				if ( tabela[  estadoDonoDaLinha ][ coluna ][j] > elemento ){
						posDeslocar = j;
						inserir = true;
				}
				j++;
		}
		
		if(posDeslocar !=  tabela[0][0].length - 1)//Ultimo elemento não precisa deslocar
				for( int i = tabela[0][0].length-1; i> posDeslocar; i-- )
						tabela[  estadoDonoDaLinha ][ coluna ][i] = tabela[  estadoDonoDaLinha ][ coluna][i-1];
	 
		tabela[  estadoDonoDaLinha ][ coluna ][posDeslocar] = elemento;
		
	}
	
	
	
	
	public static void fecholambdaRecursiva(int[][][] tabelaFNDLambda, int colunaLambda, int colunaFechoLambda, int estadoAtual, int estadoFechoLambda){
			/* Formação do fecho lambda de cada estado(linha)
			 * 
			 * Dado um estado(linha da tabela ) este metodo forma o conjunto lambda do mesmo. 
			 * Ele percorrer recursivamente chamando o metodo "fecholambdaRecursiva" passando um elento do cunjunto por vez
			 * em loop formando uma arvore de recurção.
			 
			 * Em outras palavras, para cada elemento do "conjunto Transição lambda"  da linha atual ou seja  
			 * tabela [ estadoAtual ][ colunaLambda ][...] va até seu conjunto Transição lambda" até
			 * o um caso base ( tabela [ estadoAtual ][ colunaLambda ][...] = vazio)
			 * voutando inserindo os elemento.
			 */
			
		int[][][] tabela = tabelaFNDLambda;
			
			if(tabela[ estadoAtual ][ colunaLambda ][0] == 999){//Caso base cojunto vazio 
					if( verificarExistenciaDoElementoNoCojunto(tabela, estadoFechoLambda, colunaFechoLambda , estadoAtual) == false) // verifica si ja exite o elemento no vetor  si não inserir de forma  ordenada
							inserirOrdenado(tabela, estadoFechoLambda, colunaFechoLambda , estadoAtual);
			}else{
					int i = 0;
					
					while ( tabela [ estadoAtual ][ colunaLambda ][i] != 999) {// Analisa todos elementos do conjunto lambda
							int estado =  tabela [ estadoAtual ][ colunaLambda ][i];
							
							fecholambdaRecursiva(tabela, colunaLambda, colunaFechoLambda, estado, estadoFechoLambda);	
							i++;
					}
					if( verificarExistenciaDoElementoNoCojunto(tabela, estadoFechoLambda, colunaFechoLambda , estadoAtual) ==  false)// verifica si ja exite o elemento no vetor  si não insere ordenado
							inserirOrdenado(tabela, estadoFechoLambda, colunaFechoLambda , estadoAtual);
					}
				
	}
	
	
}
