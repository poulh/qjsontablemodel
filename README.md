# qjsontablemodel

QT Table Model which takes json in 'arrays of hashes'.

```c++
QJsonTableModel::Header header;
header.push_back( QJsonTableModel::Heading( { {"title","Title"},    {"index","title"} }) );
header.push_back( QJsonTableModel::Heading( { {"title","Season"},   {"index","season"} }) );
header.push_back( QJsonTableModel::Heading( { {"title","Episode"},  {"index","episode"} }) );
header.push_back( QJsonTableModel::Heading( { {"title","Air Date"}, {"index","air_date"} }) );

episodes = new QJsonTableModel( header, this );
ui->episodeTableView->setModel( episodes );
        
QString json = "[{\"series\":\"Black Sails\",\"season\":1,\"episode\":1,\"title\":\"I.\",\"air_date\":\"2014-01-25\"},{\"series\":\"Black Sails\",\"season\":1,\"episode\":2,\"title\":\"II.\",\"air_date\":\"2014-02-01\"}]";
QJsonDocument jsonDocument = QJsonDocument::fromJson( json );
episodes->setJson( jsonDocument );
```        
