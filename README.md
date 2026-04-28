# railway-reservation-system
class RailwayReservationSystem:
    def __init__(self):
        self.total_seats = 10
        self.available_seats = self.total_seats
        self.reservations = {}
        self.ticket_counter = 1

    def check_availability(self):
        print(f"\nAvailable Seats: {self.available_seats}")

    def book_ticket(self):
        if self.available_seats <= 0:
            print("\nNo seats available!")
            return

        name = input("Enter passenger name: ")
        seats = int(input("Enter number of seats to book: "))

        if seats > self.available_seats:
            print("\nNot enough seats available!")
            return

        ticket_id = self.ticket_counter
        self.reservations[ticket_id] = {
            "name": name,
            "seats": seats
        }

        self.available_seats -= seats
        self.ticket_counter += 1

        print(f"\nTicket booked successfully! Ticket ID: {ticket_id}")

    def view_reservation(self):
        ticket_id = int(input("Enter Ticket ID: "))

        if ticket_id in self.reservations:
            res = self.reservations[ticket_id]
            print("\nReservation Details:")
            print(f"Name: {res['name']}")
            print(f"Seats Booked: {res['seats']}")
        else:
            print("\nInvalid Ticket ID!")

    def cancel_ticket(self):
        ticket_id = int(input("Enter Ticket ID to cancel: "))

        if ticket_id in self.reservations:
            seats = self.reservations[ticket_id]["seats"]
            self.available_seats += seats
            del self.reservations[ticket_id]
            print("\nTicket cancelled successfully!")
        else:
            print("\nInvalid Ticket ID!")

    def menu(self):
        while True:
            print("\n--- Railway Reservation System ---")
            print("1. Check Seat Availability")
            print("2. Book Ticket")
            print("3. View Reservation")
            print("4. Cancel Ticket")
            print("5. Exit")

            choice = input("Enter your choice: ")

            if choice == '1':
                self.check_availability()
            elif choice == '2':
                self.book_ticket()
            elif choice == '3':
                self.view_reservation()
            elif choice == '4':
                self.cancel_ticket()
            elif choice == '5':
                print("\nThank you!")
                break
            else:
                print("\nInvalid choice!")



if __name__ == "__main__":
    system = RailwayReservationSystem()
    system.menu()
