// Estructura del laboratorio: com.poo.lab4
// Incluye: core, workers, app


// =========================
// Archivo: com/poo/lab4/core/CuentaBancaria.java
// =========================
package com.poo.lab4.core;


public class CuentaBancaria {
private double saldo;


public CuentaBancaria(double saldoInicial) {
this.saldo = saldoInicial;
}


public synchronized void transaccion(double monto, String usuario) {
try {
System.out.println("Usuario " + usuario + " realizando transacción: " + monto);
double temp = saldo + monto;
Thread.sleep(200); // Simula latencia
saldo = temp;
System.out.println("Nuevo saldo tras transacción de " + usuario + ": " + saldo);
} catch (InterruptedException e) {
e.printStackTrace();
}
}


public double getSaldo() {
return saldo;
}
}




// =========================
// Archivo: com/poo/lab4/workers/CajeroRunnable.java
// =========================
package com.poo.lab4.workers;


import com.poo.lab4.core.CuentaBancaria;


public class CajeroRunnable implements Runnable {


private CuentaBancaria cuenta;
private double monto;
private String usuario;


public CajeroRunnable(CuentaBancaria cuenta, double monto, String usuario) {
this.cuenta = cuenta;
this.monto = monto;
this.usuario = usuario;
}


@Override
public void run() {
cuenta.transaccion(monto, usuario);
}
}




// =========================
// Archivo: com/poo/lab4/app/MainBanco.java
// =========================
package com.poo.lab4.app;


import com.poo.lab4.core.CuentaBancaria;
import com.poo.lab4.workers.CajeroRunnable;


import java.io.DataOutputStream;
import java.io.FileOutputStream;


public class MainBanco {
public static void main(String[] args) {
}
