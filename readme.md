## Porque Usar o IONIC? 

  Componentes prontos com facilidade para implementação e todo o suporte e documentação necessário. 
  - Facilidade para Desenvolver 
  - Multiplas Plataformas (Android/IOS)
  

## Cuidados 

Quanto maior o numero de blibliotecas no seu package.json maior vai ser para manter atualizado no futuro. 



## Baixar o Android Studio 
    
https://developer.android.com/studio?hl=pt-br

## Pré-Requistios

- Angular CLI Instalado
- NPM Instalado 
- Ter criado algum projeto em Angular 
- Saber trabalhar com REST Protheus 
# Extensão VSCODE 

https://marketplace.visualstudio.com/items?itemName=ionic.ionic

## Adicionar o IONIC no projeto 
    
https://ionicframework.com/docs/angular/your-first-app

### Passo a Passo

```
node -v
npm -v
```

### Instalar IONIC 

```    
npm install -g @ionic/cli
``` 

###  Abrir Projeto 

Iniciar projeto com um template

```
ionic start treinamento-advpl-poui-angular-ionic --type=angular
```

Opcional: Inicia o projeto com um template em branco 

```
ionic start treinamento-advpl-poui-angular-ionic blank --type=angular
```

> treinamento-advpl-poui-angular-ionic => Nome do projeto

## Adicionar o Capacitor ao Projeto 

```
ionic integrations enable capacitor
```

## Adicionar a Plataforma Android 
  
```
ionic capacitor add android
```

## Adicionar Plugin Nativo Camera 
```
npm install @capacitor/camera
```

Código:
```
import { Camera, CameraResultType } from '@capacitor/camera';

const takePicture = async () => {
  const image = await Camera.getPhoto({
    quality: 90,
    allowEditing: false,
    resultType: CameraResultType.Uri
  });

  const imageUrl = image.webPath;
  // Use o imageUrl em um elemento <img>
};
```

## Adicionar Leitor de Codigo de Barras

```
npm install @capacitor-community/barcode-scanner
```

Sincroniza com o capacitor
```
npx cap sync
```

### Configurar permissão do Android 

1. Abra o arquivo android/app/src/main/AndroidManifest.xml.
2. Adicione a permissão de câmera dentro da tag <manifest>:

```
<uses-permission android:name="android.permission.CAMERA" />
```

### Codigo 
```
import { Component } from '@angular/core';
import { BarcodeScanner } from '@capacitor-community/barcode-scanner';

@Component({
  selector: 'app-home',
  templateUrl: 'home.page.html',
  styleUrls: ['home.page.scss'],
})
export class HomePage {

  constructor() {}

  async startScan() {
    // Verifica se tem permissão
    const status = await BarcodeScanner.checkPermission({ force: true });

    if (status.granted) {
      // Começa o scanner
      await BarcodeScanner.hideBackground(); // Oculta o fundo da webview
      const result = await BarcodeScanner.startScan(); // Inicia a leitura

      // Se o resultado não foi cancelado, exibe o conteúdo
      if (result.hasContent) {
        console.log(result.content); // O conteúdo do QR code ou código de barras
        alert(`Código escaneado: ${result.content}`);
      }
    } else {
      // Solicita permissão se necessário
      alert('Permissão para usar a câmera foi negada');
    }
  }

  stopScan() {
    BarcodeScanner.stopScan(); // Para o scanner se for necessário
  }
}
```

## Adicionar o PO-UI no Projeto 

Preciso? Não, entretanto você pode usar vários componentes em conjunto com o Angular e PO-UI 

```
ng add @po-ui/ng-components
```

### Testar 
```
ionic capacitor run android
```

## Executar o IONIC Server
ionic serve



## Build Projeto 

```
ionic build
```

## Sync Projeto  com Capacitor 

```
ionic capacitor sync
```

## Abrir o Android Studio 
```
ionic capacitor open android
```

### AVD Manager (Android Virtual Device Manager) 

Ferramenta dentro do Android Studio que utilizamos para Simular 



## Android

### Debugar

#### Executar e Depurar o Aplicativo

Utilizar o Android Studio para Depurar 

```
npx cap open android
```
> Para esse Comando funcionar precisar que o Android Studio esteja instalado e com o AVD esteja configurado

#### Chrome 

Usar o Chrome DevTools (opcional)

`chrome://inspect`

#### Monitor de LOGS 
Monitorar Logs

### Permissão para se comunicar com HTTP sem HTTPS 

Por padrão o Android somente deixa comunicação com HTTPS (REST), no cenário onde precisamos se comunicar internamente com HTTP, em uma rede interna precisamos habilitar isso no `AndroidManifest.xml`

> Para conexão externa (Fora da Rede do cliente) utilize sempre HTTPS com boas práticas de segurança 


## IOS 
Para gerar o APP para IOS é necessário MAC 
