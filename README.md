# 
from pymodbus.client import ModbusTcpClient

# 1. Ustvarimo klienta
client = ModbusTcpClient(
    host="192.168.1.100",
    port=502,
    timeout=3
)

# 2. Povežemo se s PLC-jem
if client.connect():

    print("Povezava uspešna!")

    # 3. Preberemo 10 holding registrov
    result = client.read_holding_registers(
        address=0,
        count=10,
        slave=1
    )

    # 4. Preverimo rezultat
    if not result.isError():
        print("Prebrane vrednosti:")
        print(result.registers)
    else:
        print("Napaka pri branju!")

    # 5. Zapremo povezavo
    client.close()

else:
    print("Povezava s PLC ni uspela!")
