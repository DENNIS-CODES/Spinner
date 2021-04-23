## Spinner
`Spinners` provide a quick way to select one value from a set. In the default state, a spinner shows its currently selected value. Touching the spinner displays a dropdown menu with all other available values, from which the user can select a new one

![image](https://user-images.githubusercontent.com/65861136/115913226-fe098680-a478-11eb-899d-235fdcde1a11.png)

# a spinner Adapter App
You can add a spinner to your layout with the Spinner object. You should usually do so in your XML layout with a `<Spinner>` element. For example:

```
<Spinner
    android:id="@+id/planets_spinner"
    android:layout_width="match_parent"
    android:layout_height="wrap_content" />
```    
To populate the spinner with a list of choices, you then need to specify a `SpinnerAdapter` in your `Activity` or `Fragment` source code.
The choices you provide for the spinner can come from any source, but must be provided through an `SpinnerAdapter`, such as an `ArrayAdapter` if the choices are available in an `array` or a `CursorAdapter` if the choices are available from a database query.


Key classes are the following:

- Spinner
- SpinnerAdapter
- AdapterView.OnItemSelectedListener

With an array such as this one, you can use the following code in your `Activity` or `Fragment` to supply the spinner with the array using an instance of `ArrayAdapter`:

```
JAVA

Spinner spinner = (Spinner) findViewById(R.id.spinner);
// Create an ArrayAdapter using the string array and a default spinner layout
ArrayAdapter<CharSequence> adapter = ArrayAdapter.createFromResource(this,
        R.array.planets_array, android.R.layout.simple_spinner_item);
// Specify the layout to use when the list of choices appears
adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
// Apply the adapter to the spinner
spinner.setAdapter(adapter);
```
The `createFromResource()` method allows you to create an `ArrayAdapter` from the `string array`. The third argument for this method is a layout resource that defines how the selected choice appears in the `spinner control`. The `simple_spinner_item` layout is provided by the platform and is the default layout you should use unless you'd like to define your own layout for the spinner's appearance.

You should then call `setDropDownViewResource(int)` to specify the layout the adapter should use to display the list of spinner choices `(simple_spinner_dropdown_item` is another standard layout defined by the platform).

Call `setAdapter()` to apply the adapter to your Spinner.

# Responding to User Selections
When the user selects an item from the drop-down, the Spinner object receives an on-item-selected event.

To define the selection event handler for a spinner, implement the `AdapterView.OnItemSelectedListener` interface and the corresponding `onItemSelected()` callback method. For example, here's an implementation of the interface in an Activity:

```
JAVA

public class SpinnerActivity extends Activity implements OnItemSelectedListener {
    ...

    public void onItemSelected(AdapterView<?> parent, View view,
            int pos, long id) {
        // An item was selected. You can retrieve the selected item using
        // parent.getItemAtPosition(pos)
    }

    public void onNothingSelected(AdapterView<?> parent) {
        // Another interface callback
    }
}
```

The `AdapterView.OnItemSelectedListener` requires the `onItemSelected()` and `onNothingSelected()` callback methods.

Then you need to specify the interface implementation by calling `setOnItemSelectedListener():`

```
JAVA

Spinner spinner = (Spinner) findViewById(R.id.spinner);
spinner.setOnItemSelectedListener(this);
```
If you implement the `AdapterView.OnItemSelectedListener` interface with your Activity or Fragment (such as in the example above), you can pass this as the interface instance.
