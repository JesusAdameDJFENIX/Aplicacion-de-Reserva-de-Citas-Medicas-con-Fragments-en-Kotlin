VIDEO DE EXPLICACIÓN:

https://youtu.be/LgSqYiYCXsY

1. activity_main.xml
Este es el diseño de la actividad principal (MainActivity). Utiliza un RelativeLayout que contiene una Toolbar y un FragmentContainerView.
La Toolbar se establece como la barra de acción de la aplicación, utilizando un color de fondo y un tema específicos.
El FragmentContainerView es donde se cargarán los fragments (pantallas) de la aplicación, comenzando por DoctorSelectionFragment.


<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <androidx.appcompat.widget.Toolbar
        android:id="@+id/toolbar"
        android:layout_width="match_parent"
        android:layout_height="?attr/actionBarSize"
        android:background="?attr/colorPrimary"
        android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar" />


    <androidx.fragment.app.FragmentContainerView
        android:id="@+id/fragment_container_view"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_below="@id/toolbar" />
</RelativeLayout>

![image](https://github.com/user-attachments/assets/0ab65fc3-7fff-4420-b7f6-5684d4d6e82f)


2. MainActivity.kt
MainActivity es la actividad principal de la aplicación.
Se inicializa el ViewModel compartido para manejar la información que se pasará entre los fragments.
La Toolbar se configura para ser la barra de acción de la actividad.
Si es la primera vez que se crea la actividad, se carga el DoctorSelectionFragment.



package com.example.reservadecitasmdicas

import androidx.lifecycle.ViewModelProvider
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import androidx.appcompat.widget.Toolbar

class MainActivity : AppCompatActivity() {
    private lateinit var viewModel: SharedViewModel

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)


        val toolbar: Toolbar = findViewById(R.id.toolbar)
        setSupportActionBar(toolbar)


        viewModel = ViewModelProvider(this).get(SharedViewModel::class.java)

        
        if (savedInstanceState == null) {
            supportFragmentManager.beginTransaction()
                .replace(R.id.fragment_container_view, DoctorSelectionFragment())
                .commit()
        }
    }
}

![image](https://github.com/user-attachments/assets/d4d62d6f-6571-4c40-97ee-473e939f7723)


3.fragment_doctor_selection.xml

Este fragmento contiene un RecyclerView que se usará para mostrar una lista de doctores.
Se utiliza un LinearLayout para organizar los elementos en una columna vertica



<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recyclerView_doctors"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
</LinearLayout>

![image](https://github.com/user-attachments/assets/46b174a7-3b86-4586-8b8c-31f5ae08d353)


4. fragment_appointment_details.xml

Este fragmento permite al usuario ver el nombre y especialidad del doctor seleccionado y elegir una fecha y hora para la cita.
Incluye un DatePicker para seleccionar la fecha y un TimePicker para seleccionar la hora.
Un botón "Siguiente" se utiliza para avanzar a la siguiente pantalla.



<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:id="@+id/textView_doctor_name"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Nombre del Doctor" />

    <TextView
        android:id="@+id/textView_doctor_specialty"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Especialidad" />

    <DatePicker
        android:id="@+id/datePicker"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />

    <TimePicker
        android:id="@+id/timePicker"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />

    <Button
        android:id="@+id/button_next"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Siguiente" />
</LinearLayout>


![image](https://github.com/user-attachments/assets/de94687e-48aa-464e-a334-935b58e6388c)


5. fragment_confirmation.xml

Este fragmento muestra la información de la cita que se va a confirmar, incluyendo el nombre del doctor, 
especialidad, fecha y hora de la cita.
Un botón "Confirmar" permite al usuario confirmar la cita.



<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:id="@+id/textView_doctor_name"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Nombre del Doctor" />

    <TextView
        android:id="@+id/textView_doctor_specialty"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Especialidad" />

    <TextView
        android:id="@+id/textView_appointment_date"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Fecha" />

    <TextView
        android:id="@+id/textView_appointment_time"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hora" />

    <Button
        android:id="@+id/button_confirm"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Confirmar" />
</LinearLayout>

![image](https://github.com/user-attachments/assets/eeb5ba69-7bc5-4a87-9195-f6d818358eae)

6. item_doctor.xml

Este diseño representa un ítem individual en la lista de doctores que se muestra en el RecyclerView.
Contiene dos TextView que muestran el nombre y la especialidad del doctor.



<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:padding="16dp">

    <TextView
        android:id="@+id/textView_doctor_name"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Nombre del Doctor" />

    <TextView
        android:id="@+id/textView_doctor_specialty"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Especialidad" />
</LinearLayout>


![image](https://github.com/user-attachments/assets/4e1a7dcd-1bc6-4ba1-b0a3-b6680b42f633)


7. Doctor.kt
Este es un modelo de datos (data class) que representa a un doctor,
incluyendo su nombre, especialidad y disponibilidad.


package com.example.reservadecitasmdicas

data class Doctor(
    val name: String,
    val specialty: String,
    val availability: String
)


![image](https://github.com/user-attachments/assets/b4a02728-3fb3-4b30-95de-c0a0d7192a8b)


8. DoctorAdapter.kt

DoctorAdapter es un adaptador para el RecyclerView, encargado de mostrar la lista de doctores.
El método onBindViewHolder vincula los datos del doctor a los elementos de la vista 
y establece un listener para la selección del doctor.


package com.example.reservadecitasmdicas

import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.TextView
import androidx.recyclerview.widget.RecyclerView

class DoctorAdapter(
    private val doctors: List<Doctor>,
    private val onDoctorSelected: (Doctor) -> Unit
) : RecyclerView.Adapter<DoctorAdapter.DoctorViewHolder>() {

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): DoctorViewHolder {
        val view = LayoutInflater.from(parent.context).inflate(R.layout.item_doctor, parent, false)
        return DoctorViewHolder(view)
    }

    override fun onBindViewHolder(holder: DoctorViewHolder, position: Int) {
        val doctor = doctors[position]
        holder.bind(doctor)
        holder.itemView.setOnClickListener {
            onDoctorSelected(doctor)
        }
    }

    override fun getItemCount(): Int = doctors.size

    class DoctorViewHolder(itemView: View) : RecyclerView.ViewHolder(itemView) {
        private val nameTextView: TextView = itemView.findViewById(R.id.textView_doctor_name)
        private val specialtyTextView: TextView = itemView.findViewById(R.id.textView_doctor_specialty)

        fun bind(doctor: Doctor) {
            nameTextView.text = doctor.name
            specialtyTextView.text = doctor.specialty
        }
    }
}

![image](https://github.com/user-attachments/assets/a790b784-5e1f-4b15-b721-d459f16db75f)


9. SharedViewModel.kt

SharedViewModel es una clase que extiende ViewModel, diseñada para mantener y 
gestionar datos relacionados con la UI durante cambios de configuración, como la rotación de pantalla.
selectedDoctor: Un MutableLiveData que almacena el doctor seleccionado.
Permite observar cambios en el doctor elegido desde diferentes fragments.
appointmentDate: Un MutableLiveData que almacena la fecha de la cita.
appointmentTime: Un MutableLiveData que almacena la hora de la cita.

package com.example.reservadecitasmdicas

import androidx.lifecycle.MutableLiveData
import androidx.lifecycle.ViewModel

class SharedViewModel : ViewModel() {
    val selectedDoctor = MutableLiveData<Doctor>()
    val appointmentDate = MutableLiveData<String>()
    val appointmentTime = MutableLiveData<String>()
}

![image](https://github.com/user-attachments/assets/74cd170f-d1aa-4534-a634-a59a6c202605)

10. DoctorSelectionFragment.kt

DoctorSelectionFragment es un fragmento que permite a los usuarios seleccionar un doctor de una lista.
Utiliza un RecyclerView para mostrar la lista de doctores. 
El LinearLayoutManager se usa para mostrar los elementos de manera vertical.
Al seleccionar un doctor, se almacena en el ViewModel compartido (SharedViewModel) 
y se navega al AppointmentDetailsFragment para continuar con la reserva de la cita.

package com.example.reservadecitasmdicas

import android.os.Bundle
import androidx.fragment.app.Fragment
import androidx.lifecycle.ViewModelProvider
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import androidx.recyclerview.widget.LinearLayoutManager
import androidx.recyclerview.widget.RecyclerView

class DoctorSelectionFragment : Fragment() {

    private lateinit var viewModel: SharedViewModel

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        val view = inflater.inflate(R.layout.fragment_doctor_selection, container, false)


        viewModel = ViewModelProvider(requireActivity()).get(SharedViewModel::class.java)


        val recyclerView = view.findViewById<RecyclerView>(R.id.recyclerView_doctors)
        recyclerView.layoutManager = LinearLayoutManager(requireContext())
        recyclerView.adapter = DoctorAdapter(getDoctors(), onDoctorSelected)

        return view
    }


    private fun getDoctors(): List<Doctor> {
        return listOf(
            Doctor("Dr. John Doe", "Cardiología", "Disponible"),
            Doctor("Dra. Jane Smith", "Dermatología", "Disponible"),

        )
    }


    private val onDoctorSelected: (Doctor) -> Unit = { doctor ->
        viewModel.selectedDoctor.value = doctor


        parentFragmentManager.beginTransaction()
            .replace(R.id.fragment_container_view, AppointmentDetailsFragment())
            .addToBackStack(null)
            .commit()
    }
}

![image](https://github.com/user-attachments/assets/284b028c-047c-48cc-8469-595bb8b00e29)

![image](https://github.com/user-attachments/assets/7b87d55e-7dad-4bbc-89eb-ebd4b431547e)


11. AppointmentDetailsFragment

AppointmentDetailsFragment permite a los usuarios seleccionar la fecha 
y hora para la cita con el doctor previamente elegido.

Muestra el nombre y especialidad del doctor usando TextView.
Utiliza DatePicker y TimePicker para que el usuario elija la fecha y hora.

Cuando el usuario hace clic en el botón "Siguiente", se almacenan los valores de fecha y hora en el ViewModel 
y se navega al ConfirmationFragment.



package com.example.reservadecitasmdicas

import android.os.Bundle
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.Button
import android.widget.DatePicker
import android.widget.TextView
import android.widget.TimePicker
import androidx.fragment.app.Fragment
import androidx.lifecycle.ViewModelProvider

class AppointmentDetailsFragment : Fragment() {

    private lateinit var viewModel: SharedViewModel
    private lateinit var datePicker: DatePicker
    private lateinit var timePicker: TimePicker

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        val view = inflater.inflate(R.layout.fragment_appointment_details, container, false)


        viewModel = ViewModelProvider(requireActivity()).get(SharedViewModel::class.java)


        val doctorNameTextView = view.findViewById<TextView>(R.id.textView_doctor_name)
        val doctorSpecialtyTextView = view.findViewById<TextView>(R.id.textView_doctor_specialty)
        val selectedDoctor = viewModel.selectedDoctor.value
        doctorNameTextView.text = selectedDoctor?.name
        doctorSpecialtyTextView.text = selectedDoctor?.specialty


        datePicker = view.findViewById(R.id.datePicker)
        timePicker = view.findViewById(R.id.timePicker)


        val nextButton = view.findViewById<Button>(R.id.button_next)
        nextButton.setOnClickListener {

            val date = "${datePicker.dayOfMonth}/${datePicker.month + 1}/${datePicker.year}"
            val time = "${timePicker.hour}:${timePicker.minute}"

            viewModel.appointmentDate.value = date
            viewModel.appointmentTime.value = time


            parentFragmentManager.beginTransaction()
                .replace(R.id.fragment_container_view, ConfirmationFragment())
                .addToBackStack(null)
                .commit()
        }

        return view
    }


    


![image](https://github.com/user-attachments/assets/4b240d0f-2d6c-414d-b447-6f410befcbde)

![image](https://github.com/user-attachments/assets/fa103099-1f65-4fa9-a296-d38d1b3cf675)


12. ConfirmationFragment

ConfirmationFragment muestra un resumen de la cita antes de confirmarla.
Muestra el nombre y especialidad del doctor, junto con la fecha y hora seleccionadas, usando TextView.
Al hacer clic en el botón "Confirmar", se muestra un Toast que indica que la cita ha sido confirmada.


package com.example.reservadecitasmdicas

import android.os.Bundle
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.Button
import android.widget.TextView
import android.widget.Toast
import androidx.fragment.app.Fragment
import androidx.lifecycle.ViewModelProvider

class ConfirmationFragment : Fragment() {

    private lateinit var viewModel: SharedViewModel

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        val view = inflater.inflate(R.layout.fragment_confirmation, container, false)


        viewModel = ViewModelProvider(requireActivity()).get(SharedViewModel::class.java)


        val doctorNameTextView = view.findViewById<TextView>(R.id.textView_doctor_name)
        val doctorSpecialtyTextView = view.findViewById<TextView>(R.id.textView_doctor_specialty)
        val dateTextView = view.findViewById<TextView>(R.id.textView_appointment_date)
        val timeTextView = view.findViewById<TextView>(R.id.textView_appointment_time)

        doctorNameTextView.text = viewModel.selectedDoctor.value?.name
        doctorSpecialtyTextView.text = viewModel.selectedDoctor.value?.specialty
        dateTextView.text = viewModel.appointmentDate.value
        timeTextView.text = viewModel.appointmentTime.value


        val confirmButton = view.findViewById<Button>(R.id.button_confirm)
        confirmButton.setOnClickListener {
            Toast.makeText(requireContext(), "Cita confirmada", Toast.LENGTH_SHORT).show()
        }

        return view
    }
}

![image](https://github.com/user-attachments/assets/60644d55-bcfc-4340-b1ad-3dc116c41781)

![image](https://github.com/user-attachments/assets/d4bc7d7e-0cca-490c-8113-b5430baed607)

Resumen
Estos fragmentos forman parte de una aplicación para la reserva de citas médicas.

DoctorSelectionFragment: Permite al usuario seleccionar un doctor.
AppointmentDetailsFragment: Permite al usuario seleccionar la fecha y hora para la cita.
ConfirmationFragment: Muestra un resumen de la cita y permite confirmar la reserva.
Cada fragmento interactúa con el SharedViewModel para almacenar y recuperar datos entre las diferentes pantallas.

Y por ultimo este es el resultado final 


![Grabación-2024-10-20-132454](https://github.com/user-attachments/assets/1609335f-7b76-4cee-ba25-b47d21363a3f)


![Grabación-2-2024-10-20-132737](https://github.com/user-attachments/assets/0baf1273-fb98-46ca-9891-2748de66462d)


![Grabación-3-2024-10-20-133127](https://github.com/user-attachments/assets/327e821b-e5ae-44da-af60-39bc9ec150cd)




