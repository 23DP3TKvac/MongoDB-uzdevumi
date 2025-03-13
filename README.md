
# MongoDB-uzdevumi

## Uzdevums 1
Izveidot datubāzi ar nosaukumu school:

use school;

## Uzdevums 2
Izveidot kolekciju students datubāzē school:

db.createCollection("students");

## Uzdevums 3
Pievienot dokumentus kolekcijā students:

db.students.insertMany([
    { "name": "Anna", "age": 15, "grade": 9, "subjects": ["math", "science"] },
    { "name": "John", "age": 16, "grade": 10, "subjects": ["history", "art"] },
    { "name": "Lisa", "age": 14, "grade": 8, "subjects": ["music", "english"] }
]);

## Uzdevums 4
Atrodi visus studentus no kolekcijas students:

db.students.find();

## Uzdevums 5
Atrodi studentu ar vārdu "Anna":

db.students.find({ "name": "Anna" });

## Uzdevums 6
Atrodi visus studentus, kuriem ir vecums 15:

db.students.find({ "age": 15 });

## Uzdevums 7
Atrodi studentus, kuriem ir klase (grade) 10:

db.students.find({ "grade": 10 });

## Uzdevums 8
Atrodi studentus, kuriem ir vecums lielāks par 14:

db.students.find({ "age": { $gt: 14 } });

## Uzdevums 9
Atrodi studentus, kuriem ir klase mazāka vai vienāda ar 9:

db.students.find({ "grade": { $lte: 9 } });

## Uzdevums 10
Atrodi studentus, kuriem ir vecums starp 14 un 16 (ieskaitot robežas):

db.students.find({ "age": { $gte: 14, $lte: 16 } });

## Uzdevums 11
Atrodi studentus, kuru vārdi sākas ar burtu "A":

db.students.find({ "name": /^A/ });

## Uzdevums 12
Atrodi studentus, kuriem ir priekšmets "math" savā subjects masīvā:

db.students.find({ "subjects": "math" });

## Uzdevums 13
Atrodi studentus, kuriem ir vismaz viens no šādiem priekšmetiem: "science" vai "art":

db.students.find({ "subjects": { $in: ["science", "art"] } });

## Uzdevums 14
Atrodi studentus, kuriem nav priekšmeta "history":

db.students.find({ "subjects": { $nin: ["history"] } });

## Uzdevums 15
Atrodi visus studentu vārdus un vecumus, bet neiekļaujiet citus datus:

db.students.find({}, { "name": 1, "age": 1, "_id": 0 });

## Uzdevums 16
Atrodi visus studentus un iegūsti tikai to name un grade laukus:

db.students.find({}, { "name": 1, "grade": 1, "_id": 0 });

## Uzdevums 17
Atrodi visus studentus un sakārto tos pēc vecuma augošā secībā:

db.students.find().sort({ "age": 1 });

## Uzdevums 18
Atrodi visus studentus un sakārto tos pēc vārda dilstošā secībā:

db.students.find().sort({ "name": -1 });

## Uzdevums 19
Atrodi visus studentus un sakārto tos pirmajā pa vecumu, otrajā pa vārdu:

db.students.find().sort({ "age": 1, "name": 1 });

## Uzdevums 20
Pārakstīt studenta "Anna" vecumu uz 16:

db.students.updateOne(
    { "name": "Anna" },
    { $set: { "age": 16 } }
);

## Uzdevums 21
Pievienot jaunu priekšmetu "biology" studentam "John":

db.students.updateOne(
    { "name": "John" },
    { $push: { "subjects": "biology" } }
);

## Uzdevums 22
Mainīt visiem studentiem klasi uz 11:

db.students.updateMany(
    {},
    { $set: { "grade": 11 } }
);

## Uzdevums 23
Dzēst studentu ar vārdu "Lisa":

db.students.deleteOne({ "name": "Lisa" });

## Uzdevums 24
Dzēst visus studentus, kuriem ir vecums mazāks par 15:

db.students.deleteMany({ "age": { $lt: 15 } });

## Uzdevums 25
Aprēķināt vidējo vecumu visiem studentiem:

db.students.aggregate([
    { $group: { _id: null, avgAge: { $avg: "$age" } } }
]);

## Uzdevums 26
Aptuveni cik studentu ir katrā klases līmenī (grade):

db.students.aggregate([
    { $group: { _id: "$grade", count: { $sum: 1 } } }
]);

## Uzdevums 27
Izveidot sarakstu ar visiem unikāliem priekšmetiem (subjects), ko māca studenti:

db.students.aggregate([
    { $unwind: "$subjects" },
    { $group: { _id: "$subjects" } }
]);
