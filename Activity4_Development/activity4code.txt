signature_price = 2
tracking_price = 5

while True:
    name = input("Enter the customer's name: ")
    address = input("Enter the customer's address: ")
    phone = input("Enter the customer's phone number: ")
    if name == "" or address == "":
        print("The name and address cannot be left blank")
        continue
    if not phone.isdigit() or len(phone) != 11:
        print("The phone number must be 11 numbers long")
        continue
    break

while True:
    number_of_parcels = input("How many parcels are being collected (1 to 6): ")
    if not number_of_parcels.isdigit():
        print("Please enter a whole number")
        continue
    number_of_parcels = int(number_of_parcels)
    if number_of_parcels < 1 or number_of_parcels > 6:
        print("The number of parcels must be between 1 and 6")
        continue
    break

total_cost = 0
receipt = []

parcel = 1
while parcel <= number_of_parcels:
    print("Parcel", parcel)
    try:
        height = int(input("Enter the height in cm: "))
        length = int(input("Enter the length in cm: "))
        width = int(input("Enter the width in cm: "))
        weight = float(input("Enter the weight in kg: "))
    except ValueError:
        print("Please enter numbers only, the height, length and width must be whole numbers")
        continue
    if height <= 0 or length <= 0 or width <= 0 or weight <= 0:
        print("The measurements and weight must be more than 0")
        continue

    size = height + length + width

    if size > 450 or weight > 30:
        print("Parcel can't be collected, please enter the parcel again")
        continue

    if size > 150 or weight > 15:
        parcel_cost = 30
    elif size >= 95 or weight > 2:
        parcel_cost = 20
    else:
        parcel_cost = 5
    receipt.append("Parcel " + str(parcel) + ": size " + str(size) + "cm, weight " + str(weight) + "kg - £" + format(parcel_cost, ".2f"))

    while True:
        signature = input("Do you want signature on delivery for £2? (Y/N): ").upper()
        if signature == "Y" or signature == "N":
            break
        print("Please enter Y or N")
    if signature == "Y":
        parcel_cost = parcel_cost + signature_price
        receipt.append("   Signature on delivery - £" + format(signature_price, ".2f"))

    while True:
        tracking = input("Do you want parcel tracking for £5? (Y/N): ").upper()
        if tracking == "Y" or tracking == "N":
            break
        print("Please enter Y or N")
    if tracking == "Y":
        parcel_cost = parcel_cost + tracking_price
        receipt.append("   Parcel tracking - £" + format(tracking_price, ".2f"))

    receipt.append("   Parcel " + str(parcel) + " cost - £" + format(parcel_cost, ".2f"))
    total_cost = total_cost + parcel_cost
    parcel = parcel + 1

print()
print("COLLECTION RECEIPT")
print("Name:", name)
print("Address:", address)
print("Phone number:", phone)
print("Number of parcels:", number_of_parcels)
for line in receipt:
    print(line)
print("----------------------------------------")
print("Total cost of collection: £" + format(total_cost, ".2f"))
