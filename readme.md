# Instalación

Para instalar el paquete de idioma Español a SugarCRM se puede hacer de dos formas: 

1. Descarga el archivo ZIP de uno de los Tags (Releases) de este repositorio y súbelo a tu SugarCRM mediante "Module Loader".

2. Para instalar con git deploy crea un git remoto en producción. Por ejemplo en /home/crm/git con git init --bare SugarSpanishLanguage y luego agrega el remoto como "live" en la copia de trabajo. Luego en el remoto live crea el archivo hooks/post-receive que se ejecutará con cada push a dicho remoto. 

El contenido de este hooks/post-receive sería este:

```
#!/bin/bash
export GIT_WORK_TREE=/home/crm/git/checkout
VERSION=$(git tag | sort -V | tail -1)
echo "DEPLOYING $VERSION"
git checkout -f $VERSION
cd /home/crm/git/checkout/
zip -r /home/crm/crm-www/upload/upgrades/langpack/SugarCRM-Spanish-$VERSION.zip *
cp manifest.php /home/crm/crm-www/upload/upgrades/langpack/SugarCRM-Spanish-$VERSION-manifest.php
rm -rf /home/crm/git/checkout/*
```

La ejecución de este hook genera el archivo Zip que puede ser instalado desde Module Builder.

# ¿Cómo colaborar a este proyecto?

IMPORTANTE: Se usa GitFlow.

1. Clona el repositorio y opera en el branch develop ( git checkout develop) y trabaja en tu copia de trabajo integrando tus feature-branches hacia develop.

2. Sube los cambios empujando develop hacia el origin develop y avisa al administrador para integrar el commit hacia el master y generar cada cierto tiempo un release tag.

NOTA: Los tag release usan la siguiente nomenclatura: VERSION-DE-SUGAR-CRM-VERSION-DEL-LENGUAJE: Ejemplo: SugarCrm-6.5-SpanishLanguagePack-1.2.1     Números de Release: Mayor.Menor.Hotfix

CRÉDITOS: pokoli es el creador de los archivos traducidos.