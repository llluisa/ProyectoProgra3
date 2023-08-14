# ProyectoProgra3
import java.util.ArrayList;
import java.util.Scanner;

class Reservation {
    int reservationNumber;
    String service;
    int numPersons;
    int hour;
    double totalCost;
}

public class ProyectoNailsSalon {
    private final ArrayList<Reservation> reservations;
    private int nextReservationNumber;

    public ProyectoNailsSalon() {
        reservations = new ArrayList<>();
        nextReservationNumber = 1;
    }

    public void displayMenu() {
        System.out.println("1. Login");
        System.out.println("2. Módulo de reservas");
        System.out.println("3. Módulo de facturación");
        System.out.println("4. Salir");
    }

    public void makeReservation() {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Servicios disponibles:");
        System.out.println("1. Pedicure (20,000 colones)");
        System.out.println("2. Manicure (10,000 colones)");
        System.out.println("3. Manicure con esmaltado (17,000 colones)");
        System.out.println("4. Pedicure con esmaltado (27,000 colones)");

        System.out.print("Seleccione el tipo de servicio: ");
        int serviceChoice = scanner.nextInt();
        System.out.print("Cantidad de personas: ");
        int numPersons = scanner.nextInt();

        int[] hourChoices = { 8, 11, 13, 15 };
        System.out.println("Horarios disponibles: 8 am, 11 am, 1 pm, 3 pm");
        System.out.println("Seleccione el horario:");
        for (int i = 0; i < hourChoices.length; i++) {
            System.out.println((i + 1) + ". " + hourChoices[i] + " am");
        }
        int hourChoiceIndex = scanner.nextInt();
        int hourChoice = hourChoices[hourChoiceIndex - 1];

        if ((serviceChoice == 1 || serviceChoice == 2) && numPersons > 1) {
            System.out.println("Lo siento, solo se permite 1 persona por espacio para este servicio.");
            return;
        }
        if (serviceChoice == 4 && numPersons > 1) {
            System.out.println("Lo siento, solo se permite 1 persona por espacio para el servicio de Pedicure con esmaltado.");
            return;
        }

        String[] serviceNames = { "Pedicure", "Manicure", "Manicure con esmaltado", "Pedicure con esmaltado" };
        double[] serviceCost = { 20000, 10000, 17000, 27000 };
        String selectedService = serviceNames[serviceChoice - 1];
        double totalCost = numPersons * serviceCost[serviceChoice - 1];

        Reservation reservation = new Reservation();
        reservation.reservationNumber = nextReservationNumber;
        reservation.service = selectedService;
        reservation.numPersons = numPersons;
        reservation.hour = hourChoice;
        reservation.totalCost = totalCost;

        reservations.add(reservation);

        System.out.println("Reservación exitosa. Su número de reservación es: " + nextReservationNumber);
        nextReservationNumber++;
    }

    public void generateInvoice() {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Ingrese el número de reservación: ");
        int reservationNumber = scanner.nextInt();

        for (Reservation reservation : reservations) {
            if (reservation.reservationNumber == reservationNumber) {
                scanner.nextLine(); // Consume newline left-over
                System.out.print("Nombre del cliente: ");
                String clientName = scanner.nextLine();
                System.out.print("Número de identificación del cliente: ");
                String clientId = scanner.nextLine();

                double iva = 0.13;
                double totalAmount = reservation.totalCost * (1 + iva);

                System.out.println("\nArt Nails Salon Ced 3-101-604064");
                System.out.println("Datos del cliente:");
                System.out.println("Nombre: " + clientName);
                System.out.println("Número de identificación: " + clientId);
                System.out.println("\nDetalles de la reserva:");
                System.out.println("Reservación #: " + reservation.reservationNumber);
                System.out.println("Servicio: " + reservation.service);
                System.out.println("Cantidad de personas: " + reservation.numPersons);
                System.out.println("Hora: " + reservation.hour + " am");
                System.out.println("Monto total: " + reservation.totalCost + " colones");
                System.out.println("Monto total con I.V.A: " + totalAmount + " colones");
                return;
            }
        }

        System.out.println("Reservación no encontrada.");
    }

    public void run() {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            displayMenu();
            System.out.print("Seleccione una opción: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    // Implementar el login si es necesario
                    break;
                case 2:
                    makeReservation();
                    break;
                case 3:
                    generateInvoice();
                    break;
                case 4:
                    System.out.println("Gracias por usar el sistema. ¡Hasta luego!");
                    System.exit(0);
                default:
                    System.out.println("Opción inválida. Por favor, seleccione una opción válida.");
            }
        }
    }

    public static void main(String[] args) {
        ProyectoNailsSalon salon = new ProyectoNailsSalon();
        salon.run();
    }
}
