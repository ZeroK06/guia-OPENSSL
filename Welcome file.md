<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Welcome file</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><h1 id="guía-sobre-encriptaron-empleando-rsa-y-openssl">Guía sobre encriptaron empleando RSA y OPENSSL</h1>
<h3 id="que-es-rsa">Que es RSA?</h3>
<p>RSA es un sistema criptográfico de clave pública</p>
<p><img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*kve33LSdO4pNj3K3cb6wKA.png" alt="Descripción de la imagen"></p>
<p>Para nosotros emplear esta tecnica de encriptacion debemos tener una llave privada y publica.</p>
<p>Pero antes esta es la estructura de un comando en consola</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token punctuation">[</span>libreria<span class="token punctuation">]</span> <span class="token punctuation">[</span>comandoDeLibreria<span class="token punctuation">]</span> <span class="token punctuation">[</span>-opcion<span class="token punctuation">]</span> <span class="token punctuation">[</span>propiedadDeLaOpcion<span class="token punctuation">]</span>
</code></pre>
<h3 id="ejemplo-de-genera-clave-privada-sin-contrasena">Ejemplo de genera clave privada (sin contrasena)</h3>
<h4 id="genrsa">genrsa</h4>
<p>comando de OPENSSL para generar clave RSA</p>
<h4 id="out-filename.pem-2048">-out filename.pem 2048</h4>
<p>genera un archivo llamado “filename”, este nombre puede ser cualquiera con la longitud de 2048 bits</p>
<pre class=" language-bash"><code class="prism  language-bash">openssl  genrsa  -out  privado.pem  2048
</code></pre>
<h3 id="ejemplo-de-generar-clave-privada-contrasena">Ejemplo de generar clave privada (contrasena)</h3>
<h4 id="aes128">-aes128</h4>
<p>especifica que se va acifrar con una contrasena</p>
<h4 id="passout-opcional">-passout (opcional)</h4>
<p>ingresa la contrasena si no la utilizas te solicitara por consola</p>
<pre class=" language-bash"><code class="prism  language-bash">openssl  genrsa  -aes128  -out  privado.pem  2048
</code></pre>
<h3 id="ejemplo-de-generar-clave-publica-con-la-clave-privada">Ejemplo de generar clave publica (con la clave privada)</h3>
<h4 id="rsa">rsa</h4>
<p>Este comando procesa claves RSA</p>
<h4 id="in-filename.pem">-in filename.pem</h4>
<p>Especifica el nombre de la llave privada</p>
<h4 id="pubout">-pubout</h4>
<p>Con esta opción se generará una clave pública.</p>
<pre class=" language-bash"><code class="prism  language-bash">openssl  rsa  -in  privado.pem  -pubout  -out  publico.pem
</code></pre>
<h2 id="ejercicio--cifrado-y-descifrar-mensaje-empleando-rsa">Ejercicio:  Cifrado y Descifrar mensaje empleando RSA</h2>
<h4 id="paso-1-generar-nuestra-llave-privada">Paso 1: Generar nuestra llave privada</h4>
<pre class=" language-bash"><code class="prism  language-bash">openssl  genrsa  -aes128  -out  privado.pem  1024
</code></pre>
<p>este comando nos solicitara una contrasena <strong>RECUERDA ESTA CONTRASENA</strong></p>
<h4 id="paso-2-generar-nuestra-llave-publica">Paso 2: Generar nuestra llave publica</h4>
<pre class=" language-bash"><code class="prism  language-bash">openssl  rsa -in privado.pem -pubout -out  publico.pem
</code></pre>
<p>Si nuestra clave privada tiene contrasena, ingresala.</p>
<h4 id="paso-3-cifrar-nuestro-mensajes-con-la-llave-publica">Paso 3: Cifrar nuestro mensajes con la llave publica</h4>
<pre class=" language-bash"><code class="prism  language-bash">openssl rsautl -encrypt -pubin -inkey clavePublica.pem -in textoDePrueba.txt -out textoEncriptado.enc
</code></pre>
<p>El comando <strong>rsautl</strong> se puede utilizar para firmar, verificar, cifrar y descifrar datos utilizando el algoritmo RSA.</p>
<h5 id="encrypt">-encrypt</h5>
<p>Cifre los datos de entrada utilizando una clave pública RSA.</p>
<h5 id="pubin">-pubin</h5>
<p>Cifre los datos de entrada utilizando una clave pública RSA.</p>
<h5 id="inkey-llavepublica.pem">-inkey llavePublica.pem</h5>
<p>El archivo de clave de entrada, de forma predeterminada, debe ser una clave privada RSA.</p>
<h5 id="in-archivo.txt">-in archivo.txt</h5>
<p>Especifica el archivo a encriptar</p>
<h5 id="out-archivo.enc">-out archivo.enc</h5>
<p>Especifica el archivo ya encriptado</p>
<h4 id="paso-3-descifrar-nuestro-mensaje-con-la-llave-privada">Paso 3: Descifrar nuestro mensaje con la llave privada</h4>
<pre class=" language-bash"><code class="prism  language-bash">openssl rsautl -decrypt -inkey llavePrivada.pem  -in textoEncriptado.enc
</code></pre>
<p>Si la llave privada cuenta con contrasena te solicitara escribirla</p>
<h5 id="decrypt">-decrypt</h5>
<p>Descifre los datos de entrada utilizando una clave privada RSA.</p>
</div>
</body>

</html>
