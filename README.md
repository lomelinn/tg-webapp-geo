# 📍 Telegram WebApp - Captura Segura de Ubicación

Una aplicación web moderna integrada con **Telegram WebApp API** que permite la captura segura y verificada de ubicaciones geográficas a través de bots de Telegram. Este proyecto implementa autenticación por firma URL y geolocalización de alta precisión.

![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?logo=telegram&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![WebApp](https://img.shields.io/badge/WebApp-API-blue)
![Geolocation](https://img.shields.io/badge/Geolocation-Enabled-green)

## 🎯 Descripción General

Esta WebApp de Telegram está diseñada para **desarrolladores de bots** y **sistemas de tracking** que necesitan capturar ubicaciones de usuarios de forma segura y verificada. La aplicación incluye:

- **Integración Telegram WebApp**: API oficial de Telegram para aplicaciones web
- **Autenticación por Firma**: Verificación criptográfica de URLs para prevenir ataques
- **Geolocalización Precisa**: Captura de coordenadas con alta precisión y métricas de accuracy
- **Interfaz Adaptativa**: Diseño que se adapta al tema claro/oscuro de Telegram
- **Manejo de Errores**: Logging detallado y manejo robusto de excepciones

## 🛠 Stack Tecnológico

### Frontend
- **HTML5** - Estructura semántica optimizada
- **CSS3** - Variables CSS con soporte para temas de Telegram
- **Vanilla JavaScript** - Sin dependencias externas para máximo rendimiento
- **Telegram WebApp API** - Integración nativa con Telegram

### APIs & Servicios
- **Geolocation API** - Captura de coordenadas del dispositivo
- **Telegram Bot API** - Comunicación bidireccional con bots
- **URL Signing** - Sistema de autenticación por firma criptográfica

## 📁 Estructura del Proyecto

```
telegram-webapp/
├── BotTelegram.html           # WebApp principal
├── README.md                  # Documentación del proyecto
└── assets/                    # (opcional) Assets estáticos
```

## 🚀 Configuración Rápida

### Prerrequisitos
- **Bot de Telegram** configurado con BotFather
- **HTTPS** habilitado (requerido por Telegram WebApp)
- **Servidor web** para hospedar la aplicación

### Configuración del Bot

1. **Crear bot con BotFather**
   ```
   /newbot
   /setmenubutton
   ```

2. **Configurar WebApp URL**
   ```
   Configura la URL de tu WebApp hospedada
   Ejemplo: https://tu-dominio.com/BotTelegram.html
   ```

3. **Implementar comando de ubicación**
   ```javascript
   // En tu bot, crear comando que genere URL firmada
   const signedUrl = `${webappUrl}?n=${nonce}&s=${signature}`;
   ```

## 📱 Uso de la Aplicación

### Flujo de Usuario
1. Usuario envía comando `/ubicacion` al bot
2. Bot genera URL firmada y la envía como WebApp button
3. Usuario abre la WebApp desde Telegram
4. WebApp solicita permisos de geolocalización
5. Usuario autoriza y se captura la ubicación
6. Datos se envían de vuelta al bot de forma segura

### Datos Capturados
```javascript
{
  "src": "webapp",
  "t": 1696176000000,        // timestamp
  "lat": 2,            // latitud
  "lon": -15,          // longitud  
  "acc": 12,                 // precisión en metros
  "initData": "telegram_data", // datos de autenticación
  "n": "nonce_value",        // nonce para verificación
  "s": "signature_hash"      // firma criptográfica
}
```

## 🔐 Características de Seguridad

### Autenticación por Firma URL
- **Nonce único**: Previene ataques de replay
- **Firma criptográfica**: Valida la autenticidad de la solicitud
- **Timestamp**: Evita reutilización de enlaces antiguos

### Validación de Datos
- **initData de Telegram**: Autenticación nativa de la plataforma
- **Verificación dual**: URL signing + Telegram initData
- **Logging detallado**: Seguimiento de todas las acciones

### Privacidad
- **Sin almacenamiento local**: Datos se envían directamente al bot
- **HTTPS obligatorio**: Comunicación encriptada
- **Permisos explícitos**: Usuario debe autorizar geolocalización

## 🎨 Características de UI/UX

### Diseño Adaptativo
- **Tema automático**: Detecta tema claro/oscuro de Telegram
- **Variables CSS nativas**: Usa los colores del tema de Telegram
- **Responsive design**: Optimizado para dispositivos móviles

### Experiencia de Usuario
- **Feedback visual**: Logging en tiempo real de todas las acciones
- **Estados de botones**: Previene múltiples clics accidentales
- **Mensajes informativos**: Guías claras para el usuario
- **Auto-cierre**: Se cierra automáticamente después de enviar datos

## 🔧 Configuración Avanzada

### Personalización de Precisión
```javascript
var opts = { 
  enableHighAccuracy: true,    // Máxima precisión GPS
  maximumAge: 0,              // Sin caché de ubicación
  timeout: 12000              // Timeout de 12 segundos
};
```

### Personalización de Tema
```css
:root { 
  color-scheme: light dark; 
}
body { 
  background: var(--tg-theme-bg-color, #0f1115);
  color: var(--tg-theme-text-color, #e8e8e8);
}
```

## 📊 Rendimiento y Métricas

### Tiempos de Respuesta
- **Carga inicial**: < 1s
- **Captura GPS**: 2-8s (dependiendo del dispositivo)
- **Envío de datos**: < 0.5s
- **Cierre automático**: 0.6s después del envío

### Precisión de Ubicación
- **GPS habilitado**: 3-10 metros
- **Wi-Fi/Red**: 10-100 metros
- **Fallback**: Red celular (100-1000 metros)

## 🔍 Debugging y Logs

### Console Logging
```javascript
console.log("[WEBAPP]", mensaje);     // Info general
console.log("[WEBAPP][LOG_ERR]", error); // Errores de logging
```

### Estados de la Aplicación
- ✅ **WebApp lista**: Inicialización correcta
- ✅ **initData OK**: Autenticación de Telegram válida  
- ✅ **Firma URL presente**: Verificación de firma exitosa
- ❌ **Error states**: Problemas de permisos, red, o autenticación

## 🚨 Troubleshooting

### Problemas Comunes

**"initData AUSENTE"**
- Solución: Abrir desde el botón del bot, no directamente en navegador

**"Error de geolocalización"** 
- Solución: Verificar permisos de ubicación en Telegram/navegador

**"sendData no disponible"**
- Solución: Confirmar que se está ejecutando dentro de Telegram WebApp

## 📋 Casos de Uso

### Aplicaciones Empresariales
- **Tracking de empleados**: Registro de ubicación para nómina
- **Logística**: Confirmación de entregas y rutas
- **Seguridad**: Check-ins en ubicaciones específicas

### Servicios al Cliente
- **Servicios a domicilio**: Confirmación de ubicación del cliente
- **Delivery**: Tracking en tiempo real de repartidores
- **Emergencias**: Captura rápida de ubicación para asistencia

## 🛡 Licencia

Este proyecto es de uso privado y confidencial. Todos los derechos reservados.

---

## 👨‍💻 Acerca del Desarrollador

**Creado por Erick Lomelín**  
Product Engineer | Full-Stack Developer | Bot Developer

📧 contacto@ericklomelin.com  
🌐 [ericklomelin.com](https://www.ericklomelin.com)  
📍 San Luis Potosí, México

---

*Telegram WebApp System v1.0 - Captura segura con precisión* 🎯

## Qué incluye
- `BotTelegram.html`: WebApp principal con geolocalización
- Sistema de autenticación por firma URL
- Integración completa con Telegram WebApp API
- Manejo robusto de errores y logging detallado

## Cómo usar
```bash
# 1. Sube el archivo a tu servidor HTTPS
# 2. Configura la URL en tu bot de Telegram  
# 3. Implementa la generación de URLs firmadas en tu bot
# 4. Los usuarios pueden acceder desde el menú del bot
```
