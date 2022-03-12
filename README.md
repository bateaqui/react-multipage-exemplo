# Exemplo de React em Hospedagem Windows

Este exemplo tem como objectivo demonstrar uma aplicação de exemplo com multi páginas, simulando as rotas.

## Primeiros passos

Esta aplicação é bem simples, então não será necessário muita coisa :)

### Pré-requisitos

NodeJS
GIT

### Instalação
Instalando o NPM

    npm install

Gerando os arquivos para fazer o deploy

    npm run build

Você irá notar que tem uma pasta nova a "build", são esses arquivos de dentro da pasta build que devemos enviar para o BateAqui Host

## Configurando a Hospedagem

Para finalizar a configuração, precisamos alterar o arquivo web.config que está presente somente em hospedagens windows.
Aqui vai um exemplo de web.config para você copiar e colar.

### Rewrite

Um dos pontos que causa problema é nas rotas, para isso precisamos incluir no web.config essas linhas aqui:

    <system.webServer>
        <rewrite>
            <rules>
                <rule name="React Routes" stopProcessing="true">
                    <match url=".*" />
                    <conditions logicalGrouping="MatchAll">
                        <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
                        <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
                        <add input="{REQUEST_URI}" pattern="^/(api)" negate="true" />
                    </conditions>
                    <action type="Rewrite" url="/" />
                </rule>
            </rules>
        </rewrite>
    </system.webServer>

### Web.config completo

    ﻿<?xml version="1.0" encoding="UTF-8"?>
    <configuration>
    <system.webServer>
        <httpErrors>
            <remove statusCode="400" />
            <error statusCode="400" path="C:\Inetpub\vhosts\COLOQUE_AQUI_A_SUA_URL_TEMPORARIAr\error_docs\bad_request.html" />
            <remove statusCode="401" />
            <error statusCode="401" path="C:\Inetpub\vhosts\COLOQUE_AQUI_A_SUA_URL_TEMPORARIA\error_docs\unauthorized.html" />
            <remove statusCode="403" />
            <error statusCode="403" path="C:\Inetpub\vhosts\COLOQUE_AQUI_A_SUA_URL_TEMPORARIA\error_docs\forbidden.html" />
            <remove statusCode="404" />
            <error statusCode="404" path="C:\Inetpub\vhosts\COLOQUE_AQUI_A_SUA_URL_TEMPORARIA\error_docs\not_found.html" />
            <remove statusCode="405" />
            <error statusCode="405" path="C:\Inetpub\vhosts\COLOQUE_AQUI_A_SUA_URL_TEMPORARIA\error_docs\method_not_allowed.html" />
            <remove statusCode="406" />
            <error statusCode="406" path="C:\Inetpub\vhosts\COLOQUE_AQUI_A_SUA_URL_TEMPORARIA\error_docs\not_acceptable.html" />
            <remove statusCode="407" />
            <error statusCode="407" path="C:\Inetpub\vhosts\COLOQUE_AQUI_A_SUA_URL_TEMPORARIA\error_docs\proxy_authentication_required.html" />
            <remove statusCode="412" />
            <error statusCode="412" path="C:\Inetpub\vhosts\COLOQUE_AQUI_A_SUA_URL_TEMPORARIA\error_docs\precondition_failed.html" />
            <remove statusCode="414" />
            <error statusCode="414" path="C:\Inetpub\vhosts\COLOQUE_AQUI_A_SUA_URL_TEMPORARIA\error_docs\request-uri_too_long.html" />
            <remove statusCode="415" />
            <error statusCode="415" path="C:\Inetpub\vhosts\COLOQUE_AQUI_A_SUA_URL_TEMPORARIA\error_docs\unsupported_media_type.html" />
            <remove statusCode="500" />
            <error statusCode="500" path="C:\Inetpub\vhosts\COLOQUE_AQUI_A_SUA_URL_TEMPORARIA\error_docs\internal_server_error.html" />
            <remove statusCode="501" />
            <error statusCode="501" path="C:\Inetpub\vhosts\COLOQUE_AQUI_A_SUA_URL_TEMPORARIA\error_docs\not_implemented.html" />
            <remove statusCode="502" />
            <error statusCode="502" path="C:\Inetpub\vhosts\COLOQUE_AQUI_A_SUA_URL_TEMPORARIA\error_docs\bad_gateway.html" />
            <remove statusCode="503" />
            <error statusCode="503" path="C:\Inetpub\vhosts\COLOQUE_AQUI_A_SUA_URL_TEMPORARIA\error_docs\maintenance.html" />
        </httpErrors>
        <rewrite>
            <rules>
                <rule name="React Routes" stopProcessing="true">
                    <match url=".*" />
                    <conditions logicalGrouping="MatchAll">
                        <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
                        <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
                        <add input="{REQUEST_URI}" pattern="^/(api)" negate="true" />
                    </conditions>
                    <action type="Rewrite" url="/" />
                </rule>
            </rules>
        </rewrite>
        <tracing>
            <traceFailedRequests>
                <clear />
            </traceFailedRequests>
        </tracing>
    </system.webServer>
    <system.web>
        <compilation tempDirectory="C:\Inetpub\vhosts\COLOQUE_AQUI_A_SUA_URL_TEMPORARIA\tmp" />
    </system.web>
    </configuration>

## Observação

Lembre de alterar todos os "COLOQUE_AQUI_A_SUA_URL_TEMPORARIA" para sua url temporária que está disponível no painel do BateAqui, menu minhas assinaturas.
