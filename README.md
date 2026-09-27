### Markdown
## 🚀 Personal CachyOS + Hyprland Configuration & Setup Guide

Documentación y guía de configuración para un entorno de escritorio optimizado en **CachyOS (Arch Linux)** utilizando **Hyprland** como gestor de ventanas (Wayland), **Waybar** como barra de estado y un conjunto de herramientas para desarrollo, multimedia y productividad.

## 🛠️ 1. Instalación de Software y Aplicaciones
💬 Mensajería y Productividad


### WhatsApp WebApp / ZapZap (Cliente de escritorio)
```bash
paru -S zapzap
```

### Telegram Desktop
```bash
sudo pacman -S telegram-desktop
```

### Signal Messenger
```bash
sudo pacman -S signal-desktop
```

### Clientes multicuenta (Ferdium / Rambox)
```bash
paru -S ferdium-bin
```

## 🌐 Navegación Web

### Firefox (Versión optimizada de CachyOS) y paquete de idioma en español
```bash
sudo pacman -S firefox firefox-i18n-es-es
```

### Navegador Brave
```bash
sudo pacman -S brave-bin
```

## 📸 Captura de Pantalla y Multimedia

## Herramientas de captura (Grim + Slurp + Swappy + Portapapeles)
```bash
sudo pacman -S --needed grim slurp swappy wl-clipboard
```

### Hyprshot (Capturas automáticas para Hyprland)
```bash
paru -S hyprshot
```

### OBS Studio + Soporte para PipeWire/Wayland
```bash
sudo pacman -S --needed obs-studio pipewire-media-session xdg-desktop-portal-hyprland
```

## 🔒 Cifrado, Bóvedas y Seguridad

### Cryptomator (Protección de carpetas mediante bóvedas cifradas)
```bash
sudo pacman -S cryptomator
```

### VeraCrypt (Contenedores cifrados)
```bash
sudo pacman -S veracrypt
```

### ProtonVPN (GUI)
```bash
paru -S protonvpn-gui
```

## 🎮 Juegos

### TLauncher / Minecraft Java Edition
```bash
paru -S tlauncher
```


## 📊 2. Configuración del Entorno de Escritorio
### ⏰ Configuración de Waybar (~/.config/waybar/config.jsonc)

Ajustes para mostrar el día de la semana (%a) en el reloj y la apertura interactiva del gestor de red (nmtui) al hacer clic sobre el ícono de Wi-Fi:

### 👨🏻‍💻 JSON

{
    "layer": "top",
    "position": "top",
    "height": 34,
    "margin-top": 8,
    "margin-left": 12,
    "margin-right": 12,
    "spacing": 0,

    "modules-left": [
        "custom/launcher",
        "hyprland/workspaces"
    ],
    "modules-center": [
        "clock"
    ],
    "modules-right": [
        "pulseaudio",
        "bluetooth",
        "backlight",
        "custom/wifi",
        "custom/nightlight",
        "cpu",
        "memory",
        "custom/btop",
        "custom/power"
    ],

    // --- LEFT MODULES ---
    "custom/launcher": {
        "format": "  ",
        "tooltip": false,
        "on-click": "wofi --show drun"
    },

    "hyprland/workspaces": {
        "active-only": false,
        "all-outputs": true,
        "format": "{id}",
        "on-click": "hyprctl dispatch workspace {id}",
        "persistent-workspaces": {
            "*": [1, 2, 3, 4, 5, 6, 7]
        }
    },

    // --- CENTER MODULES ---
    "clock": {
        "format": "⏰ {:%a %H:%M  |  %m/%d/%Y}",
        "tooltip-format": "{:%Y %B}\n{calendar}"
    },

    // --- RIGHT MODULES ---
    "pulseaudio": {
        "format": "{icon} {volume}%",
        "format-muted": "󰝟 Muted",
        "format-icons": {
            "default": ["󰕿", "󰖀", "󰕾"]
        },
        "on-click": "pavucontrol"
    },

    "bluetooth": {
        "format": " {status}",
        "format-disabled": "󰂲",
        "format-connected": " {device_alias}",
        "format-connected-battery": " {device_battery_percentage}%",
        "tooltip-format": "{controller_alias}\t{controller_address}\n\n{num_connections} connected",
        "tooltip-format-connected": "{controller_alias}\t{controller_address}\n\n{num_connections} connected:\n\n{device_enumerate}",
        "tooltip-format-enumerate-connected": "{device_alias}\t{device_address}",
        "tooltip-format-enumerate-connected-battery": "{device_alias}\t{device_address}\t{device_battery_percentage}%",
        "on-click": "blueman-manager"
    },

    "backlight": {
        "format": "{icon} {percent}%",
        "format-icons": ["󰃞", "󰃟", "󰃠"]
    },

    "custom/wifi": {
        "format": "  ",
        "exec": "nmcli -t -f active,ssid dev wifi | grep '^yes' | cut -d: -f2 || echo 'Offline'",
        "interval": 5,
        "on-click": "kitty --class=wifi-window nmtui",
        "tooltip": true,
        "tooltip-format": "Click to manage Wi-Fi networks"
    },

    "cpu": {
        "format": "󰍛 {usage}%",
        "interval": 2
    },

    "memory": {
        "format": "󰘚 {percentage}%",
        "interval": 2
    },

    "custom/nightlight": {
        "format": " 󰌵 ",
        "exec": "cat /tmp/wlsunset_temp 2>/dev/null || echo 'Off'",
        "interval": 1,
        "on-click": "~/.config/waybar/scripts/nightlight.sh toggle",
        "on-scroll-up": "~/.config/waybar/scripts/nightlight.sh up",
        "on-scroll-down": "~/.config/waybar/scripts/nightlight.sh down",
        "tooltip": true,
        "tooltip-format": "Click: On/Off\nScroll: Adjust warmth (K)"
    },

    "custom/btop": {
        "format": " 󰄨 ",
        "tooltip": true,
        "tooltip-format": "Open System Monitor (btop)",
        "on-click": "kitty -e btop"
    },

    "custom/power": {
        "format": " 󰐥 ",
        "tooltip": true,
        "tooltip-format": "Power Options",
        "on-click": "wlogout"
    }
}

## 🎨 Ajustes CSS de Waybar (~/.config/waybar/style.css)
Corrección para mantener bordes estables en los hovers de los módulos:

### 👨🏻‍💻 CSS

#pulseaudio:hover,
#bluetooth:hover,
#backlight:hover,
#custom-wifi:hover,
#custom-nightlight:hover,
#network:hover,
#cpu:hover,

* {
    border: none;
    border-radius: 0;
    font-family: "JetBrainsMono Nerd Font", "Roboto", sans-serif;
    font-weight: bold;
    font-size: 13px;
    min-height: 0;
}

/* Floating bar with thin border (1px) and pronounced shadow */
window#waybar {
    background-color: rgba(22, 27, 34, 0.75);
    color: #e6edf3;
    border: 1px solid #00f5d4;
    border-radius: 8px;
    /* Outer shadow for 3D floating effect */
    box-shadow: 0px 8px 24px rgba(0, 0, 0, 0.6), 0px 0px 12px rgba(0, 245, 212, 0.35);
}

/* --- MODULE STYLES AND HOVER INTERACTIONS --- */

/* Wofi Launcher */
#custom-launcher {
    background-color: #00f5d4;
    color: #0d1117;
    padding: 0 16px;
    font-size: 16px;
    margin-right: 8px;
    border-radius: 6px 0px 10px 0px;
    transition: all 0.2s ease;
}

#custom-launcher:hover {
    background-color: #00bbf9;
    box-shadow: 0 0 10px #00bbf9;
}

/* Workspaces with glowing effect on hover */
#workspaces button {
    padding: 0 10px;
    color: #8b949e;
    background-color: rgba(33, 38, 45, 0.7);
    margin: 4px 3px;
    border-radius: 4px;
    border-bottom: 2px solid rgba(0, 245, 212, 0.2);
    transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
}

#workspaces button:hover {
    background-color: rgba(0, 245, 212, 0.25);
    color: #ffffff;
    border-bottom: 2px solid #00f5d4;
    box-shadow: 0 0 8px rgba(0, 245, 212, 0.5);
}

#workspaces button.active {
    background-color: #00bbf9;
    color: #0d1117;
    font-weight: bold;
    border-bottom: 2px solid #00f5d4;
}

/* Central Clock */
#clock {
    background-color: rgba(13, 17, 23, 0.85);
    color: #00f5d4;
    padding: 2px 18px;
    margin: 4px 0px;
    border: 1px solid #00f5d4;
    border-radius: 12px 2px 12px 2px;
    transition: all 0.3s ease;
}

#clock:hover {
    background-color: rgba(0, 245, 212, 0.15);
    box-shadow: 0 0 10px rgba(0, 245, 212, 0.4);
}

/* Right Modules Base Box Structure */
#pulseaudio,
#bluetooth,
#backlight,
#custom-wifi,
#custom-nightlight,
#network,
#cpu,
#memory {
    background-color: rgba(33, 38, 45, 0.75);
    padding: 0 10px;
    margin: 4px 2px;
    border-bottom: 2px solid #00f5d4;
    border-radius: 2px 8px 2px 8px;
    transition: all 0.25s ease;
}

/* Individual Colors for Each Module */
#pulseaudio { color: #70e000; }
#bluetooth { color: #00bbf9; }
#backlight { color: #ffb703; }
#custom-wifi { color: #38b000; }
#custom-nightlight { color: #f77f00; }
#network { color: #00bbf9; }
#cpu { color: #f72585; }
#memory { color: #4cc9f0; }

/* Unified Blue Hover Effect for Volume, Bluetooth, Wifi, Nightlight and standard modules */
#pulseaudio:hover,
#bluetooth:hover,
#backlight:hover,
#custom-wifi:hover,
#custom-nightlight:hover,
#network:hover,
#cpu:hover,
#memory:hover {
    background-color: rgba(0, 187, 249, 0.25);
/*    border: 1px solid #00bbf9; */
    border-bottom: 2px solid #00bbf9;
    box-shadow: 0 0 12px rgba(0, 187, 249, 0.6);
    color: #ffffff;
}


/* BTOP Monitor */
#custom-btop {
    background-color: rgba(0, 187, 249, 0.15);
    color: #00bbf9;
    padding: 0 10px;
    margin: 4px 2px;
    border: 1px solid #00bbf9;
    border-radius: 6px 2px 6px 2px;
    transition: all 0.2s ease;
}

#custom-btop:hover {
    background-color: #00bbf9;
    color: #0d1117;
    box-shadow: 0 0 10px #00bbf9;
}

/* Power Button */
#custom-power {
    background-color: #f72585;
    color: #ffffff;
    padding: 0 12px;
    margin: 4px 4px 4px 2px;
    border-radius: 2px 8px 2px 8px;
    transition: all 0.2s ease;
}

#custom-power:hover {
    background-color: #ff4d6d;
    box-shadow: 0 0 12px #ff4d6d;
}



## ⌨️ Atajos y Reglas de Ventanas (~/.config/hypr/hyprland.lua)

Atajos para Capturas de Pantalla:
### ---- ATAJOS DE CAPTURA DE PANTALLA --

-- Capturar pantalla completa y copiar al portapapeles (Super + Print)
```bash
hl.bind("SUPER", "Print", "exec", "grim - | wl-copy")

-- Seleccionar una región y copiar al portapapeles (Solo Print)
```bash
hl.bind("", "Print", "exec", "grim -g "$(slurp)" - | wl-copy")

-- Seleccionar área y abrir editor interactivo Swappy (Super + Shift + S)
```bash
hl.bind("SUPER_SHIFT", "S", "exec", "grim -g "$(slurp)" - | swappy -f -")

-- Captura completa guardada en carpeta usando Hyprshot (Super + Print)
```bash
hl.bind("SUPER", "Print", "exec", "hyprshot -m output -o ~/Imágenes/Capturas")

-- Captura de región guardada en carpeta usando Hyprshot (Solo Print)
```bash
hl.bind("", "Print", "exec", "hyprshot -m region -o ~/Imágenes/Capturas")


#### Reglas de Ventanas Flotantes (`window_rules`):
```lua
---- REGLAS DE VENTANAS FLOTANTES --- (~/.config/hypr/hyprland.lua)

-- Ventana flotante para la red Wi-Fi desde Waybar
hl.window_rule({
name = "wifi-float",
match = { class = "^wifi-window$" },
float = true,
})

-- Reglas para la ventana flotante de OBS Studio
hl.window_rule({
name = "obs-float",
match = { class = "^com.obsproject.Studio$" },
float = true,
})

-- Reglas para la ventana flotante de WhatsApp
hl.window_rule({
name = "whatsapp-float",
match = { class = "^.whatsapp.$" },
float = true,
})

💻 3. Comandos Útiles de Consola y Diagnóstico
⚙️ Gestión de Hyprland y Waybar
Bash
# Recargar configuración de Hyprland
hyprctl reload

# Reiniciar Waybar en segundo plano
killall waybar && waybar &

# Crear carpeta para capturas
mkdir -p ~/Imágenes/Capturas
🌐 Redes y VPN
Bash
# Consultar IP local e interfaces
ip a

# Gestor gráfico TUI para Wi-Fi
nmtui

# Escanear redes Wi-Fi
nmcli dev wifi list

# Desbloquear antenas de red (RF-kill)
sudo rfkill unblock all

# Reiniciar NetworkManager
sudo systemctl restart NetworkManager

# Restablecer interfaz tras cerrar ProtonVPN
sudo ip link set dev tun0 down 2>/dev/null
nmcli networking off && nmcli networking on

# Limpiar caché DNS
sudo resolvectl flush-caches
🖥️ Diagnóstico de Hardware y Pantalla
Bash
# Consultar información de monitores en Hyprland
hyprctl monitors

# Verificar tarjetas y controladores PCI (Red, GPU, etc.)
lspci -k | grep -iA 3 network

# Listar dispositivos USB
lsusb