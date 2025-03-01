# Python-port.s

import socket

def scan_port(target, port):
    """
    Tries to connect to a specific port on the target.
    Returns True if the port is open, False otherwise.
    """
    try:
        # Creating a socket object
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        s.settimeout(1.5)  # Increased timeout to handle slow responses

        # Trying  to connecting
        result = s.connect_ex((target, port))
        s.close()

        return result == 0  # If result is 0, the port is open
    except Exception as e:
        print(f"[!] Error scanning port {port}: {e}")
        return False

def main():
    """
    Asks the user for a target IP and scans all ports (1-65535), displaying only open ports.
    """
    print("\nSimple Python Port Scanner 🕵️‍♂️")
    target = input("Enter target IP or hostname: ")

    print(f"\nScanning {target} for open ports...\n")

    open_ports = []
    for port in range(1, 65536):
        if scan_port(target, port):
            open_ports.append(port)
            print(f"✅ Port {port} is OPEN")  # Show open ports immediately

        if port % 1000 == 0:  # Show progress every 1000 ports
            print(f"Scanning... reached port {port}")

    if not open_ports:
        print("No open ports found.")

    print("\nScan complete! 🚀")

if __name__ == "__main__":
    main()

