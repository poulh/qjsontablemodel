# QJsonTableModel

A QT JsonModel. Subclasses QT's QAbstractTableModel. Takes json in 'arrays of hashes'.  Used to populate a QTableView.

First create a header which maps each column to an index in your json object.  The order of the headings will match the Table.
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


You can then retrieve the Json object for that row via the QModelIndex. It will give you the entire row's Json object regardless of which cell you clicked.

```c++
void TVTime::on_episodesTableView_doubleClicked(const QModelIndex &index)
{
    QJsonObject object = episodes->getJsonObject( index );
    qDebug() << object["title"];
}
```
