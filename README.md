Nmea stand for National Marine Electronics Association. Most computer programs transfer the gps data into nmea format. we can convert the NMEA data to decimal Latitude and Latitude for our ease.

**Data sample:**
$GNRMC,071100.20,A,2835.9620695,N,07719.9163150,E,0.02,,220518,,,D*5A

```java
public void parseReceiveData(String nmeaData) {  
    String[] nmeaDataArray = nmeaData.split(",");  
    if (nmeaDataArray[0].equals("$GNRMC") &&  
            nmeaDataArray[3] != null &&  
            !nmeaDataArray[3].trim().isEmpty() &&  
            nmeaDataArray[5] != null &&  
            !nmeaDataArray[5].trim().isEmpty()) {  
  
        double latitude = parseToDecimal(nmeaDataArray[3], nmeaDataArray[4]);  
        double longitude = parseToDecimal(nmeaDataArray[5], nmeaDataArray[6]);    
    }  
}
```
Below is parseToDecimal method:
```java
public double parseToDecimal(String gpsData, String dir) {  
    double latLng = Double.parseDouble(gpsData);  
    if(latLng==0) return 0;  
    int dd = (int) ((float) (latLng) / 100);   
    double ss = (latLng) - dd * 100;   
    double decLatLng = dd + ss / 60;  
    if (dir.equalsIgnoreCase("w") || dir.equalsIgnoreCase("s")) {  
        return -1 * decLatLng;  
    }  
    return decLatLng;  
}
```
Now you can perform your play with latitude Longitude.
