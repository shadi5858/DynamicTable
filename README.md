# DynamicTable
This is an example of how to create a dynamic table in Angular 2+

I have two arraies called tableHead and tableColName and a data list.

    private tableColName: Array<String>=[];
    private tableHead: Array<String>=[];
    private allList : AllList[]=[];

 ngOnInit() {
 
    this.initDate();
    
 }
 
 initDate(){
 
  // calling web service to pull data from back end.
  
    this.myService.getAllData().subscribe(
      (res)=>{
        this.allList= res;                 
      },
      (err)=>{
          alertify.error('An Error has Occurred: ' + err);
      }
    );
  
  //Sample Data for allList Object
  
  [{id: 159501, residentDay: "2018-08-15", room: "D1F115", shift: "Day", occupancyId: 3109}
  
  {id: 159502, residentDay: "2018-08-16", room: "D1F115", shift: "Day", occupancyId: 3109}
  
  {id: 159503, residentDay: "2018-08-17", room: "D1F115", shift: "Day", occupancyId: 3109}
  
  {id: 159504, residentDay: "2018-08-18", room: "D1F115", shift: "Day", occupancyId: 3109}
  
  {id: 159505, residentDay: "2018-08-19", room: "D1F115", shift: "Day", occupancyId: 3109}
  
  {id: 159506, residentDay: "2018-08-20", room: "D1F115", shift: "Day", occupancyId: 3109}
  
  {id: 159507, residentDay: "2018-08-21", room: "D1F115", shift: "Day", occupancyId: 3109}
  
  {id: 159508, residentDay: "2018-08-22", room: "D1F115", shift: "Day", occupancyId: 3109}
  
  {id: 159509, residentDay: "2018-08-23", room: "D1F115", shift: "Day", occupancyId: 3109}
  ]
  
    this.allList.forEach(rd => {
                const keys = Object.keys(rd);
                for (let i = 0; i < keys.length; i++) {
                    const x = keys[i].toString();
                    if (this.tableColName.indexOf(x) === -1) {
                        this.tableColName.push(x);
                    }
                }

            });

// the result of tableColName

 ["id", "residentDay", "room", "shift", "occupancyId", "employer", "division", "subcontractor"]

            // uses this method to change the camel case to Pascal case for the table header
            this.tableColName.forEach(c => {
                this.tableHead.push(c.charAt(0).toUpperCase() + c.slice(1));
            });
            
  // the result for tableHead
  
  ["Id", "ResidentDay", "Room", "Shift", "OccupancyId", "Employer", "Division", "Subcontractor"]
            
 }
 
 Then in Html file write these codes:
 
     <table class="table table-hover" style="border: 0.15em solid lightgrey;width: 100%; font-size: 0.9em;font-weight: normal;color:#3c3d3a;">
         <thead class="title" style="background-color: lightgrey; ">

             <tr class="table-head" >
                 <th *ngFor="let t of tableHead" [class.hide]="t === 'Id' || t==='OccupancyId'" style="font-size:0.99em;">{{t}}</th>
             </tr>
             </thead>

             <tr *ngFor="let tableData of allList">
              <td *ngFor="let colName of tableColName" [class.hide]="colName === 'id' || colName === 'occupancyId'"> {{tableData[colName]}}</td>
              </tr>

      </table>



in html I used [class.hide] because did not want to show those two fields in my table.
 
