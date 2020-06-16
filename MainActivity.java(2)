public class MainActivity extends AppCompatActivity {

    RecyclerView revList;
    Button addMore;

    UserAdapter adapter;
    ArrayList<ModelClass> detailsList;
    ModelClass details;

    String Name, Profession,Age;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        revList=findViewById(R.id.recyclerview);
        addMore=findViewById(R.id.button_ADD);

        loadData();

        adapter=new UserAdapter(detailsList,this);

        addMore.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                final AlertDialog.Builder alert=new AlertDialog.Builder(MainActivity.this);
                View view = getLayoutInflater().inflate(R.layout.custom_dialouge,null);

                final EditText name=(EditText) view.findViewById(R.id.name1);
                final EditText profession=(EditText)view.findViewById(R.id.professsion1);
                final EditText age=(EditText)view.findViewById(R.id.age1);

                final Button add=view.findViewById(R.id.add_btn);
                final Button cancel=view.findViewById(R.id.cancel);






                alert.setView(view);
                final AlertDialog alertDialog=alert.create();
                alertDialog.setCanceledOnTouchOutside(false);

                add.setOnClickListener(new View.OnClickListener() {
                    @Override
                    public void onClick(View v) {

                        Name= name.getText().toString();
                        Profession= profession.getText().toString();
                        Age= age.getText().toString();

                        details=new ModelClass(Name,Profession,Age);
                        detailsList.add(details);
                        alertDialog.dismiss();
                        saveData();

                    }
                });

                cancel.setOnClickListener(new View.OnClickListener() {
                    @Override
                    public void onClick(View v) {
                        alertDialog.dismiss();
                    }
                });

                alertDialog.show();

            }
        });


        adapter.notifyItemInserted(detailsList.size()-1);
        revList.setLayoutManager(new LinearLayoutManager(this));

        ItemTouchHelper.SimpleCallback itemCallback=new ItemTouchHelper.SimpleCallback(0,ItemTouchHelper.RIGHT) {
            @Override
            public boolean onMove(@NonNull RecyclerView recyclerView, @NonNull RecyclerView.ViewHolder viewHolder, @NonNull RecyclerView.ViewHolder target) {
                return false;
            }

            @Override
            public void onSwiped(@NonNull RecyclerView.ViewHolder viewHolder, int direction) {

                detailsList.remove(viewHolder.getAdapterPosition());
                adapter.notifyDataSetChanged();

            }
        };

        new ItemTouchHelper(itemCallback).attachToRecyclerView(revList);
        revList.setAdapter(adapter);


    }

    public void saveData(){
        SharedPreferences sharedPreferences=getSharedPreferences("sharedPrefs",MODE_PRIVATE);
        SharedPreferences.Editor editor=sharedPreferences.edit();
        Gson gson=new Gson();
        String json=gson.toJson(detailsList);
        editor.putString("List",json);
        editor.apply();
    }

    public void loadData(){
        SharedPreferences sharedPreferences=getSharedPreferences("sharedPrefs",MODE_PRIVATE);
        Gson gson=new Gson();
        String json=sharedPreferences.getString("List",null);
        Type type=new TypeToken<ArrayList<ModelClass>>(){}.getType();
        detailsList=gson.fromJson(json,type);

        if (detailsList==null){
            detailsList=new ArrayList<>();
        }
    }
}
