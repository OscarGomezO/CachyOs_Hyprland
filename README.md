Bash
micro README.md
Pega el siguiente contenido dentro del archivo y guárdalo (Ctrl + S y luego Ctrl + Q):

Markdown
# 🚀 Personal CachyOS + Hyprland Configuration & Setup Guide

Documentación y guía de configuración para un entorno de escritorio optimizado en **CachyOS (Arch Linux)** utilizando **Hyprland** como gestor de ventanas (Wayland), **Waybar** como barra de estado y un conjunto de herramientas para desarrollo, multimedia y productividad.
🛠️ 1. Instalación de Software y Aplicaciones
💬 Mensajería y Productividad
Bash
# WhatsApp WebApp / ZapZap (Cliente de escritorio)
paru -S zapzap

# Telegram Desktop
sudo pacman -S telegram-desktop

# Signal Messenger
sudo pacman -S signal-desktop

# Clientes multicuenta (Ferdium / Rambox)
paru -S ferdium-bin
🌐 Navegación Web
Bash
# Firefox (Versión optimizada de CachyOS) y paquete de idioma en español
sudo pacman -S firefox firefox-i18n-es-es

# Navegador Brave
sudo pacman -S brave-bin
📸 Captura de Pantalla y Multimedia
Bash
# Herramientas de captura (Grim + Slurp + Swappy + Portapapeles)
sudo pacman -S --needed grim slurp swappy wl-clipboard

# Hyprshot (Capturas automáticas para Hyprland)
paru -S hyprshot

# OBS Studio + Soporte para PipeWire/Wayland
sudo pacman -S --needed obs-studio pipewire-media-session xdg-desktop-portal-hyprland
🔒 Cifrado, Bóvedas y Seguridad
Bash
# Cryptomator (Protección de carpetas mediante bóvedas cifradas)
sudo pacman -S cryptomator

# VeraCrypt (Contenedores cifrados)
sudo pacman -S veracrypt

# ProtonVPN (GUI)
paru -S protonvpn-gui
🎮 Juegos
Bash
# TLauncher / Minecraft Java Edition
paru -S tlauncher
📊 2. Configuración del Entorno de Escritorio
⏰ Reloj y Módulo Wi-Fi (~/.config/waybar/config.jsonc)
Ajustes para mostrar el día de la semana (%a) y la apertura interactiva del gestor de red (nmtui) al hacer clic sobre el ícono de Wi-Fi:

Code snippet
    // --- CENTER MODULES ---
    "clock": {
        "format": "⏰ {:%a %d/%m/%Y - %H:%M}",
        "tooltip-format": "{:%Y %B}\n{calendar}"
    },

    // --- RIGHT MODULES ---
    "custom/wifi": {
        "format": "  ",
        "exec": "nmcli -t -f active,ssid dev wifi | grep '^yes' | cut -d: -f2 || echo 'Offline'",
        "interval": 5,
        "on-click": "kitty --class=wifi-window nmtui",
        "tooltip": true,
        "tooltip-format": "Click to manage Wi-Fi networks"
    },
🎨 Ajustes CSS de Waybar (~/.config/waybar/style.css)
Corrección para mantener bordes estables en los hovers de los módulos:

#CSS

Bash
micro README.md
Pega el siguiente contenido dentro del archivo y guárdalo (Ctrl + S y luego Ctrl + Q):

Markdown
# 🚀 Personal CachyOS + Hyprland Configuration & Setup Guide

Documentación y guía de configuración para un entorno de escritorio optimizado en **CachyOS (Arch Linux)** utilizando **Hyprland** como gestor de ventanas (Wayland), **Waybar** como barra de estado y un conjunto de herramientas para desarrollo, multimedia y productividad.
🛠️ 1. Instalación de Software y Aplicaciones
💬 Mensajería y Productividad
Bash
# WhatsApp WebApp / ZapZap (Cliente de escritorio)
paru -S zapzap

# Telegram Desktop
sudo pacman -S telegram-desktop

# Signal Messenger
sudo pacman -S signal-desktop

# Clientes multicuenta (Ferdium / Rambox)
paru -S ferdium-bin
🌐 Navegación Web
Bash
# Firefox (Versión optimizada de CachyOS) y paquete de idioma en español
sudo pacman -S firefox firefox-i18n-es-es

# Navegador Brave
sudo pacman -S brave-bin
📸 Captura de Pantalla y Multimedia
Bash
# Herramientas de captura (Grim + Slurp + Swappy + Portapapeles)
sudo pacman -S --needed grim slurp swappy wl-clipboard

# Hyprshot (Capturas automáticas para Hyprland)
paru -S hyprshot

# OBS Studio + Soporte para PipeWire/Wayland
sudo pacman -S --needed obs-studio pipewire-media-session xdg-desktop-portal-hyprland
🔒 Cifrado, Bóvedas y Seguridad
Bash
# Cryptomator (Protección de carpetas mediante bóvedas cifradas)
sudo pacman -S cryptomator

# VeraCrypt (Contenedores cifrados)
sudo pacman -S veracrypt

# ProtonVPN (GUI)
paru -S protonvpn-gui
🎮 Juegos
Bash
# TLauncher / Minecraft Java Edition
paru -S tlauncher



📊 2. Configuración del Entorno de Escritorio
#(~/.config/waybar/config.jsonc)
#JSON

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
    /*    "network", */
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

    /*
    // --- CENTER MODULES ---
    "clock": {
        "format": "⏰ {:%H:%M  |  %m:%d:%Y}",
        "tooltip-format": "<big>{:%Y %B}</big>\n<tt><small>{calendar}</small></tt>"
    },
    */
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
        "format-disabled": "󰂲", // Disabled / Off
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

    /*
    "network": {
        "format-wifi": "󰤨 {signalStrength}%",
        "format-ethernet": "󰈀 Online",
        "format-disconnected": "󰤭 Off",
        "tooltip-format": "{ifname} via {gwaddr}"
    },
    */
    
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
        // Displays the graphical session menu (wlogout)
        "on-click": "wlogout"
    }
}



🎨 Ajustes CSS de Waybar (~/.config/waybar/style.css)
Corrección para mantener bordes estables en los hovers de los módulos:
#CSS

#pulseaudio:hover,
#bluetooth:hover,
#backlight:hover,
#custom-wifi:hover,
#custom-nightlight:hover,
#network:hover,
#cpu:hover,
#memory:hover {
    background-color: rgba(0, 187, 249, 0.25);
    border-bottom: 2px solid #00bbf9;
    box-shadow: 0 0 12px rgba(0, 187, 249, 0.6);
    color: #ffffff;
}
⌨️ Atajos y Reglas de Ventanas (~/.config/hypr/hyprland.lua)
Atajos para Capturas de Pantalla:
---- ATAJOS DE CAPTURA DE PANTALLA --

-- Capturar pantalla completa y copiar al portapapeles (Super + Print)
hl.bind("SUPER", "Print", "exec", "grim - | wl-copy")

-- Seleccionar una región y copiar al portapapeles (Solo Print)
hl.bind("", "Print", "exec", "grim -g "$(slurp)" - | wl-copy")

-- Seleccionar área y abrir editor interactivo Swappy (Super + Shift + S)
hl.bind("SUPER_SHIFT", "S", "exec", "grim -g "$(slurp)" - | swappy -f -")

-- Captura completa guardada en carpeta usando Hyprshot (Super + Print)
hl.bind("SUPER", "Print", "exec", "hyprshot -m output -o ~/Imágenes/Capturas")

-- Captura de región guardada en carpeta usando Hyprshot (Solo Print)
hl.bind("", "Print", "exec", "hyprshot -m region -o ~/Imágenes/Capturas")


#### Reglas de Ventanas Flotantes (`window_rules`):
```lua
---- REGLAS DE VENTANAS FLOTANTES ---

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




⌨️ Atajos y Reglas de Ventanas (~/.config/hypr/hyprland.lua)
Atajos para Capturas de Pantalla:
---- ATAJOS DE CAPTURA DE PANTALLA --

-- Capturar pantalla completa y copiar al portapapeles (Super + Print)
hl.bind("SUPER", "Print", "exec", "grim - | wl-copy")

-- Seleccionar una región y copiar al portapapeles (Solo Print)
hl.bind("", "Print", "exec", "grim -g "$(slurp)" - | wl-copy")

-- Seleccionar área y abrir editor interactivo Swappy (Super + Shift + S)
hl.bind("SUPER_SHIFT", "S", "exec", "grim -g "$(slurp)" - | swappy -f -")

-- Captura completa guardada en carpeta usando Hyprshot (Super + Print)
hl.bind("SUPER", "Print", "exec", "hyprshot -m output -o ~/Imágenes/Capturas")

-- Captura de región guardada en carpeta usando Hyprshot (Solo Print)
hl.bind("", "Print", "exec", "hyprshot -m region -o ~/Imágenes/Capturas")


#### Reglas de Ventanas Flotantes (`window_rules`):
```lua
---- REGLAS DE VENTANAS FLOTANTES ---

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
