#include <gtk/gtk.h>

GtkWidget *entry; // Entry widget to display and input numbers
double num1 = 0, num2 = 0;
char operation = ' '; // Initialize to space

// Function to perform the arithmetic operation
void calculate() {
    const gchar *text = gtk_entry_get_text(GTK_ENTRY(entry));
    double result = 0;
    sscanf(text, "%lf", &num2);

    switch (operation) {
        case '+':
            result = num1 + num2;
            break;
        case '-':
            result = num1 - num2;
            break;
        case '*':
            result = num1 * num2;
            break;
        case '/':
            if (num2 != 0) {
                result = num1 / num2;
            } else {
                // Handle division by zero error
                gtk_entry_set_text(GTK_ENTRY(entry), "Error");
                return;
            }
            break;
    }

    char result_str[20];
    snprintf(result_str, sizeof(result_str), "%.2lf", result);
    gtk_entry_set_text(GTK_ENTRY(entry), result_str);
    num1 = result;
    operation = ' '; // Reset operation after calculation
}

// Button click event handlers
void on_button_clicked(GtkWidget *button, gpointer data) {
    const gchar *label = gtk_button_get_label(GTK_BUTTON(button));
    const gchar *text = gtk_entry_get_text(GTK_ENTRY(entry));

    if (label[0] >= '0' && label[0] <= '9') {
        gchar new_text[100];
        g_snprintf(new_text, sizeof(new_text), "%s%s", text, label);
        gtk_entry_set_text(GTK_ENTRY(entry), new_text);
    } else if (label[0] == '=') {
        calculate();
    } else {
        // Handle operators +, -, *, /
        num1 = atof(text);
        operation = label[0];
        gtk_entry_set_text(GTK_ENTRY(entry), "");
    }
}

void on_clear_clicked(GtkWidget *button, gpointer data) {
    gtk_entry_set_text(GTK_ENTRY(entry), "");
    num1 = num2 = 0;
    operation = ' ';
}

int main(int argc, char *argv[]) {
    gtk_init(&argc, &argv);

    GtkWidget *window;
    GtkWidget *grid;
    GtkWidget *button;

    // Create the main window
    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_window_set_title(GTK_WINDOW(window), "Simple Calculator");
    gtk_container_set_border_width(GTK_CONTAINER(window), 10);
    gtk_window_set_default_size(GTK_WINDOW(window), 300, 400);
    g_signal_connect(G_OBJECT(window), "destroy", G_CALLBACK(gtk_main_quit), NULL);

    // Create a grid to arrange widgets
    grid = gtk_grid_new();
    gtk_container_add(GTK_CONTAINER(window), grid);

    // Create an entry field
    entry = gtk_entry_new();
    gtk_entry_set_alignment(GTK_ENTRY(entry), 1); // Right-align text
    gtk_grid_attach(GTK_GRID(grid), entry, 0, 0, 4, 1);

    // Create buttons
    char *button_labels[] = {"7", "8", "9", "+", "4", "5", "6", "-", "1", "2", "3", "*", "C", "0", "=", "/"};
    int button_row = 1;
    int button_col = 0;

    for (int i = 0; i < 16; i++) {
        button = gtk_button_new_with_label(button_labels[i]);
        g_signal_connect(button, "clicked", G_CALLBACK(on_button_clicked), NULL);
        gtk_grid_attach(GTK_GRID(grid), button, button_col, button_row, 1, 1);
        button_col++;
        if (button_col > 3) {
            button_col = 0;
            button_row++;
        }
    }

    // Show all widgets
    gtk_widget_show_all(window);

    // Start the GTK main loop
    gtk_main();

    return 0;
}
