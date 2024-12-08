# Curso Cardboard

## Proyecto Unity

🔧 **Consideraciones**

- Este proyecto ha sido creado utilizando **Unity 2022.3.24f1 LTS**.
- 🚫 El plugin **no soporta Unity 6**. Aunque la aplicación puede compilarse, al ejecutarla se presentan los siguientes errores:
  ```
  java.lang.ClassNotFoundException: com.google.cardboard.sdk.qrcode.CardboardParamsUtils
  java.lang.ClassNotFoundException: com.google.cardboard.sdk.QrCodeCaptureActivity
  ```

📄 Por favor, asegúrate de usar la versión recomendada de Unity para evitar problemas de compatibilidad.


## 📖 Capitulos

- [Capitulo 1](#capítulo-1--realidad-virtual-google-cardboard-tutorial-unity---configuración)
- [Capitulo 2](#capítulo-2--vr-cardboard-selección-con-la-mirada---sin-controles)
- [Capitulo 3](#capítulo-3-cardboard-vr---interacción-con-botones)
- [Capitulo 4](#capítulo-4-cómo-usar-teletransportación-en-cardboard)

## 📞 Contacto

- **🐼 [Discord](https://discord.gg/TBjZuCSmG2)**
- **🐦 [Twitter / X ](https://twitter.com/UnityAdventure)**
- **📷 [Instagram](https://www.instagram.com/unity_adventure)**


## Capítulo 1 : Realidad Virtual Google Cardboard Tutorial Unity - Configuración
⬇️ ⬇️

🔗 [Ver video tutorial gratis en YouTube](https://youtu.be/CwgOl1JAyeY) 🎥


- En este momento, la versión descargada del SDK de Cardboard es 🔗[**v1.26.0**](https://github.com/googlevr/cardboard-xr-plugin/releases/tag/v1.26.0).  
Al instalarlo, Unity solicitará activar el nuevo sistema de entrada (Input System). Es necesario aceptar, y Unity se reiniciará automáticamente. 🔄
<img src="./DocAssets/image-0.png" alt="Imagen de referencia" width="400" />

**Player Settings**
- **Minium API Level**: Android 8.0 "Oreo" (API level 26).  
- **Target API Level**: Android 13.0 (API level 33)
![alt text](./DocAssets/image-1.png)
- No es necesario modificar el archivo `AndroidManifest`. ✅

📌 **Nota importante:** Desde la grabación del video, el SDK ha tenido algunos cambios. Para probar la escena y activar las interaciones, será necesario realizar algunos pasos adicionales:  

1. Abre el menú **Layers** y selecciona **Edit Layers...**.  
2. Define una nueva capa llamada **"Interactive"**.  
3. Haz clic en el objeto **Treasure GameObject** para abrir la ventana del Inspector.  
   - Asigna su capa a **"Interactive"**.  
   - Si aparece una ventana emergente preguntando si deseas aplicar el cambio a los objetos secundarios, selecciona **"Yes, change children"**. ✅  
4. Haz clic en **Player > Camera > CardboardReticlePointer GameObject** para abrir el Inspector.  
   - En el script **"Cardboard Reticle Pointer"**, selecciona **"Interactive"** como la máscara de capa de interacción (Reticle Interaction Layer Mask). 🎯  

Al hacer esto el SDK te permitira utilizar el recticle:
- Estado normal 🔴
- Al entrar en contacto con un objeto interactable: ⭕

![alt text](./DocAssets/image-2.png)

¡Listo! Ahora tu proyecto debería estar configurado correctamente. 🚀

## Capítulo 2 : VR Cardboard SELECCIÓN con la mirada - SIN CONTROLES
⬇️ ⬇️

🔗 [Ver video tutorial gratis en YouTube](https://youtu.be/q5AvXfoGAyg) 🎥

En la nueva versión del SDK, la cámara incluye como hijo una nueva implementación llamada `CardboardReticlePointer`, que reemplaza al antiguo `CameraPointer`.  

Para seguir el tutorial del video, es necesario **desactivar** o **eliminar** el prefab `CardboardReticlePointer` en la jerarquía:  

![Referencia visual](./DocAssets/image-3.png)  

📌 En el video, se utiliza el antiguo `CameraPointer` como base.  
Para seguir el tutorial al pie de la letra, aquí tienes el código de `CameraPointer`:

```csharp
using System.Collections;
using UnityEngine;

public class CameraPointer : MonoBehaviour
{
    private const float _maxDistance = 10;
    private GameObject _gazedAtObject = null;

    public void Update()
    {

        RaycastHit hit;
        if (Physics.Raycast(transform.position, transform.forward, out hit, _maxDistance))
        {
            if (_gazedAtObject != hit.transform.gameObject)
            {
                _gazedAtObject?.SendMessage("OnPointerExit");
                _gazedAtObject = hit.transform.gameObject;
                _gazedAtObject.SendMessage("OnPointerEnter");
            }
        }
        else
        {
            _gazedAtObject?.SendMessage("OnPointerExit");
            _gazedAtObject = null;
        }
        if (Google.XR.Cardboard.Api.IsTriggerPressed)
        {
            _gazedAtObject?.SendMessage("OnPointerClick");
        }
    }
}
```

👾 **Tips adicionales**: 
- Este código permite manejar eventos como `OnPointerEnter`, `OnPointerExit` y `OnPointerClick` para los objetos con los que el usuario interactúa en la escena.  
- Recuerda que para interactuar con objecto debes agregarle un collider y el tag `Interactable`

## Capítulo 3: Cardboard VR - Interacción con Botones
⬇️ ⬇️
🔗 [Ver video tutorial gratis en YouTube](https://youtu.be/hu1bMy6woN8) 🎥

Este capítulo se seguir sin ningún problema, no existe cambio alguno. ✨

Recuerda que al momento de crear la interacción de los objetos a partir de los toggles, se debe seleccionar la opción `SetActive` de la parte superior, en donde está `Dynamic bool`.

![Referencia visual](./DocAssets/image-4.png)  

## Capítulo 4: ¿Cómo usar Teletransportación en Cardboard?

⬇️ ⬇️

🔗 [Ver video tutorial gratis en YouTube](https://youtu.be/7uZvH-7F-d4) 🎥

Este capítulo se seguir sin ningún problema, no existe cambio alguno. ✨
