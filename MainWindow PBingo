using Gtk;
using System;
using System.Collections.Generic;
using System.Diagnostics;

public partial class MainWindow: Gtk.Window
{	

	private List<int> numeros = new List<int>();

	private Random random = new Random();

	private Table table;
	private Table tableExtraidos;
	private List<Button> buttons = new List<Button>();

	private static readonly Gdk.Color COLOR_GREEN = new Gdk.Color(0, 255, 0);

	private int numeroTotalBolas = 90;

	public MainWindow (): base (Gtk.WindowType.Toplevel)
	{
		Build ();

		//uint numeroTotalFilas = ((uint)numeroTotalBolas - 1) / 10 + 1;

		table = new Table(1, 1, true);
		vbox1.Add(table);
		table.Visible = true;

		tableExtraidos = new Table(9, 10, true);
		vbox1.Add (tableExtraidos);
		tableExtraidos.Visible = true;


		addButtons ();

		for (int numero = 1; numero <= numeroTotalBolas; numero++)
		numeros.Add (numero);
		showNumeros();

		goForwardAction.Activated += delegate {

			int indexAleatorio = random.Next(numeros.Count);
			int numeroExtraido = numeros[ indexAleatorio ];

			entryNumero.Text = numeroExtraido.ToString();
			espeak(numeroExtraido);		

			buttons[numeroExtraido - 1].ModifyBg (StateType.Normal, COLOR_GREEN);

			addButtonExtraido ();

			numeros.Remove(numeroExtraido);

			showNumeros();
		};

	}

	/// <summary>
	/// Añade los botones en la tabla.
	/// </summary>
	private void addButtons() {
		for (int index = 0; index < numeroTotalBolas; index++) {

			Button button = new Button();
			button.Label = string.Format ("{0}", index + 1);
			button.Visible = true;

			buttons.Add (button);

			uint fila = (uint)index / 10;
			uint columna = (uint)index % 10;

			table.Attach(button, columna, columna + 1, fila, fila + 1);
		}
	}

	private void addButtonExtraido() {
		Button button = new Button();
		button.Label = entryNumero.Text;
		button.Visible = true;

		int index = tableExtraidos.Children.Length;

		uint fila = (uint)index / 10;
		uint columna = (uint)index % 10;
		tableExtraidos.Attach(button, columna, columna + 1, fila, fila + 1);
	}

	private void showNumeros() {
		//		for (int index = 0; index < numeros.Count; index++)
		//			Console.Write ( numeros[index] + " " );
		//		Console.WriteLine ();

		foreach (int numero in numeros)
			Console.Write( numero + " ");
		Console.WriteLine ();
	}

	private void espeak(int numeroExtraido) {
		string numeroCantado = numeroExtraido.ToString ();
		if (numeroCantado.Length > 1) {
			string digitos = numeroCantado;
			foreach (char digito in digitos) 
				numeroCantado = numeroCantado + " " + digito;
		}

		Process.Start ("espeak", "-v es \"" + numeroCantado + "\"");
	}

	protected void OnDeleteEvent (object sender, DeleteEventArgs a)
	{
		Application.Quit ();
		a.RetVal = true;
	}
}
