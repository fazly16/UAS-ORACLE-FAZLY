### UAS PDT(Pemrosesan Data Tersebar)

Membuat Aplikasi Pembelian dan Penjualan dengan menggunakan database Oracle, System Administrator menggunakan CodeIgniter dan Interface di Mobile Apps (Android). Komunikasi data antar Aplikasi menggunakan _RESTful Service_ di oracle.

### Requirement

- [Virtual Box](https://www.virtualbox.org/wiki/Downloads) (Virtual Server)
- [Oracle Developer Day 11g](https://www.oracle.com/technetwork/database/enterprise-edition/databaseappdev-vm-161299.html) (Database)
- [Android Studio](https://developer.android.com/studio) (Android IDE)
- [Codeigniter](https://www.codeigniter.com/) (Framework PHP)

### Tutorial
---------------------------
### Database
Aplikasi ini memiliki 5 table, yaitu :

1. [Customer](#table-customer)
2. [Barang](#table-barang)
3. [Penjualan](#table-penjualan)
4. [Pembelian](#table-pembelian)
5. [Supplier](#table-supplier)

### Table Barang
![Table Customer!](./BARANG/T_BARANG2.png "Table Customer")

### Table Customer
![Table Customer!](./CUSTOMER/T_CUSTOMER2.png "Table Customer")

###  Table Penjualan
![Table Customer!](./PENJUALAN/T_PENJUALAN2.png "Table Customer")

###  Table Pembelian
![Table Customer!](./PEMBELIAN/T_PEMBELIAN2.png "Table Customer")

### Table Supplier
![Table Customer!](./SUPPLIER/T_SUPPLIER2.png "Table Customer")


###  RESTful Service
![Table Customer!](./T_PEMBELIAN2.png "Table Customer")

###  
PUT dan DELETE menggunakan {id} untuk mengidentifikasi data yang akan dieksekusi.  
Metode HTTP yang digunakan dalam aplikasi ini adalah:

| Method | Description |
| ------ | ------ |
| **GET** | menyediakan hanya akses baca pada _resource_ |
| **POST** | digunakan untuk menciptakan _resource_ baru |
| **PUT** | digunakan untuk memperbarui _resource_ yang ada atau membuat _resource_ baru |
| **DELETE** | digunakan untuk menghapus _resource_ |


###  *RESTful Service* pada Barang
- **GET Barang**
![Table Customer!](./BARANG/GET_BARANG.png "Table Customer")

- **POST Barang**
![Table Customer!](./BARANG/POST_BARANG.png "Table Customer")

- **PUT Barang**
![Table Customer!](./BARANG/PUT_BARANG.png "Table Customer")

- **DELETE Barang**
![Table Customer!](./BARANG/DELETE_BARANG.png "Table Customer")

### *RESTful Service* pada Customer
- **GET Customer**
![Table Customer!](./CUSTOMER/GET_CUSTOMER.png "Table Customer")

- **POST Customer**
![Table Customer!](./CUSTOMER/POST_CUSTOMER.png "Table Customer")

- **PUT Customer**
![Table Customer!](./CUSTOMER/PUT_CUSTOMER.png "Table Customer")

- **DELETE Customer**
![Table Customer!](./CUSTOMER/DELETE_CUSTOMER.png "Table Customer")

### *RESTful Service* pada Penjualan
- **GET_Penjualan**
![Table Customer!](./PENJUALAN/GET_PENJUALAN.png "Table Customer")

- **POST_Penjualan**
![Table Customer!](./PENJUALAN/POST_PENJUALAN.png "Table Customer")



### *RESTful Service* pada Pembelian
- **GET_Pembelian**
![Table Customer!](./PEMBELIAN/GET_PEMBELIAN.png "Table Customer")

- **POST_Pembelian**
![Table Customer!](./PEMBELIAN/POST_PEMBELIAN.png "Table Customer")



### *RESTful Service* pada Supplier
- **GET Supplier**
![Table Customer!](./SUPPLIER/GET_SUPPLIER.png "Table Customer")

- **POST Supplier**
![Table Customer!](./SUPPLIER/POST_SUPPLIER.png "Table Customer")

- **PUT Supplier**
![Table Customer!](./SUPPLIER/PUT_SUPPLIER.png "Table Customer")

- **DELETE Supplier**
![Table Customer!](./SUPPLIER/DELETE_SUPPLIER.png "Table Customer")

### CodeIgniter

[Script](https://github.com/residwi/oracle-uas/blob/master/oracle-uas/application/libraries/Api.php)  dibawah ini merupakan script php yang digunakan untuk mengakses  _RESTful Services_  dari Oracle menggunakan library  [Goutte](https://github.com/FriendsOfPHP/Goutte).

```php
use GuzzleHttp\Client;

defined('BASEPATH') or exit('No direct script access allowed');

class Api
{
    private $client;

    public function __construct()
    {
        // base url yang digunakan untuk mengakses RESTful API
        $this->client = new Client(['base_uri' => 'http://192.168.43.75:8888/apex/obe/']);
    }

    public function request($method, $uri, $data = [])
    {
        // data di convert menjadi data JSON
        $options['json'] = $data;

        // jika metode HTTP nya adalah DELETE maka response yang diberikan adalah status code nya
        if ($method == 'delete') {
            $request = $this->client->request($method, $uri);
            return $request->getStatusCode();
        }

        $request = $this->client->request($method, $uri, $options);

        // response yang diberikan berupa content nya
        return $request->getBody()->getContents();
    }
}
```


#### Tampilan Web

- Barang
![List Barang](./BARANG/T_BARANG.png)

- Customer
![List Customer](./CUSTOMER/T_CUSTOMER.png)

- Penjualan
![List Penjualan](./PENJUALAN/T_PENJUALAN.png)

- Pembelian
![List Pembelian](./PEMBELIAN/T_PEMBELIAN.png)

- Supplier
![List Supplier](./SUPPLIER/T_SUPPLIER.png)

### License
Copyright © 2019, [Muhammad Fazly Qusyairy](https://github.com/residwi).
Released under the [MIT License](LICENSE).