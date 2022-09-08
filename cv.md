# Roma Tereshchenko

![It's me](./img/_119449972_10.jpg)  

*Contacts:*  
[Instagram](https://instagram.com/romchik_netyt/)  
[VK](https://vk.com/romchik_netyt/)  
[Phone](https://instagram.com/romchik_netyt/) 

***

## About me:  
I am a beginner programmer who is learning c#. I am learning how to create console and mobile applications. In the future, I would like to write a backend for websites and beautiful mobile applications. 

***

## Skills:
* C#
* Xamarin
* HTML/CSS
* Entity Framework  
* SQL 
## Code examples:
```
class BusController
    {
        readonly AutoParkDbContext db;
        public Bus Bus { get; set; }
        public BusController(DataGridView dataGridView)
        {
            db = new AutoParkDbContext();
            db.Buses.Load();
            dataGridView.DataSource = db.Buses.Local.ToBindingList();
        }
        public void Add(int number, int route, DateTime departure, DateTime arrival)
        {
            if (!db.Buses.Any(b => b.Number == number))
            {
                Bus = new Bus(number, route, departure, arrival);
                db.Buses.Add(Bus);
                Save("Новый автобус добавлен");
            }
            else
            {
                MessageBox.Show("Данный автобус уже существует");
            }
        }
        public void Save(string text)
        {
            db.SaveChanges();
            MessageBox.Show(text);
        }
        public DateTime MinDeparture() => db.Buses.Min(b => b.Departure);
        public DateTime MaxArrival() => db.Buses.Max(b => b.Arrival);
        public Bus FindById(int id) => db.Buses.Find(id);
        public void Remove(Bus bus)
        {
            db.Buses.Remove(bus);
            Save("Автобус удалён");
        }

         public partial class DriversForm : Form
    {
        readonly DriverController driverController;
        public DriversForm()
        {
            InitializeComponent();

            try
            {
                driverController = new DriverController(dataGridView1);
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
        }

        private void DriversForm_Load(object sender, EventArgs e)
        {

        }

        private void buttonAdd_Click(object sender, EventArgs e)
        {
            try
            {
                NewDriverForm newDriverForm = new NewDriverForm();
                DialogResult result = newDriverForm.ShowDialog();
                if (result == DialogResult.Cancel)
                    return;

                driverController.Add(newDriverForm.textBoxFullName.Text,
                                    (int)newDriverForm.numericUpDownWorkExperience.Value,
                                     int.Parse(newDriverForm.comboBoxClass.SelectedItem.ToString()));
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
        }

        private void buttonChange_Click(object sender, EventArgs e)
        {
            if (dataGridView1.SelectedRows.Count > 0)
            {
                try
                {
                    int index = dataGridView1.SelectedRows[0].Index;
                    if (!int.TryParse(dataGridView1[0, index].Value.ToString(), out int id))
                        return;

                    var driver = driverController.FindById(id);
                    NewDriverForm newDriverForm = new NewDriverForm();

                    newDriverForm.textBoxFullName.Text = driver.FullName;
                    newDriverForm.numericUpDownWorkExperience.Value = driver.WorkExperience;
                    newDriverForm.comboBoxClass.Text = driver.Class.ToString();

                    DialogResult result = newDriverForm.ShowDialog();
                    if (result == DialogResult.Cancel)
                        return;

                    driver.FullName = newDriverForm.textBoxFullName.Text;
                    driver.WorkExperience = (int)newDriverForm.numericUpDownWorkExperience.Value;
                    driver.Class = int.Parse(newDriverForm.comboBoxClass.SelectedItem.ToString());

                    driverController.Save("Данные о водителе изменены");
                    dataGridView1.Refresh();
                }
                catch (Exception ex)
                {
                    MessageBox.Show(ex.Message);
                }
            }
        }

        private void buttonDelete_Click(object sender, EventArgs e)
        {
            if (dataGridView1.SelectedRows.Count > 0)
            {
                int index = dataGridView1.SelectedRows[0].Index;
                if (!int.TryParse(dataGridView1[0, index].Value.ToString(), out int id))
                    return;

                driverController.Remove(driverController.FindById(id));
            }
        }
``` 

*** 
## [My CV](/%D0%A2%D0%98%D0%9F_1/cv.md)
***

## My trainings:
No completed trainings  
## English level:
A2+