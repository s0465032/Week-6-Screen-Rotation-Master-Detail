//
//  MasterViewController.swift
//  MyFavBands
//
//  Created by Charles Konkol on 2/14/15.
//  Copyright (c) 2015 Rock Valley College. All rights reserved.
//

import UIKit

class MasterViewController: UITableViewController {

    
    var detailViewController: DetailViewController? = nil
//1) Comment out
    //var objects = NSMutableArray()
    
    
//2) Create new MSMutableArray
    var listArray = NSMutableArray()


    override func awakeFromNib() {
        super.awakeFromNib()
        self.clearsSelectionOnViewWillAppear = false
        self.preferredContentSize = CGSize(width: 320.0, height: 600.0)
    }
   
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view, typically from a nib.
        
//3) Comment out edit button
        //self.navigationItem.leftBarButtonItem = self.editButtonItem()
        
//4) Populate Array of band names from images you downloaded. Names must match file names without file extenstion .jpg
        
listArray = ["Joe Cocker","Leonard Skynard","Eagles","Journey", "38 Special","Miranda Lambert", "Little Big Town","Band Perry"]
        
//5) Comment out Add Button - 2 lines
        
//        let addButton = UIBarButtonItem(barButtonSystemItem: .Add, target: self, action: "insertNewObject:")
//        self.navigationItem.rightBarButtonItem = addButton
        
//6) Add Title
        title = "My Favorite Bands"
       
        let controllers = self.splitViewController!.viewControllers
        self.detailViewController = controllers[controllers.count-1].topViewController as? DetailViewController
    }

    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }

    
//7) Comment out Insert Function
    
//    func insertNewObject(sender: AnyObject) {
//        objects.insertObject(NSDate(), atIndex: 0)
//        let indexPath = NSIndexPath(forRow: 0, inSection: 0)
//        self.tableView.insertRowsAtIndexPaths([indexPath], withRowAnimation: .Automatic)
//    }

    // MARK: - Segues

    override func prepareForSegue(segue: UIStoryboardSegue, sender: AnyObject?) {
        if segue.identifier == "showDetail" {
            if let indexPath = self.tableView.indexPathForSelectedRow() {
//8) Replace object with listArray and NSDate with NSString
                let object = listArray[indexPath.row] as NSString
                let controller = (segue.destinationViewController as UINavigationController).topViewController as DetailViewController
                
//9) Add 3 lines of code to populate Name and URL. Ignore Error lines
                controller.detailItem = object
                 controller.productName = object
                controller.productURL = object + ".jpg"
                
                controller.navigationItem.leftBarButtonItem = self.splitViewController?.displayModeButtonItem()
                controller.navigationItem.leftItemsSupplementBackButton = true
                
//10) Add to hide Menu after tap
                self.splitViewController?.toggleMasterView()
            }
        }
    }

    // MARK: - Table View

    override func numberOfSectionsInTableView(tableView: UITableView) -> Int {
        return 1
    }

    override func tableView(tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
 //11 Comment Out
        
        // return objects.count
//12) Add Code
        return listArray.count
        
    }

    override func tableView(tableView: UITableView, cellForRowAtIndexPath indexPath: NSIndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCellWithIdentifier("Cell", forIndexPath: indexPath) as UITableViewCell

        let object = listArray[indexPath.row] as NSString
        cell.textLabel.text = object.description
        return cell
    }

//13) Comment out override func tableView
//    override func tableView(tableView: UITableView, canEditRowAtIndexPath indexPath: NSIndexPath) -> Bool {
//        // Return false if you do not want the specified item to be editable.
//        return true
//    }

//14) Comment out override func tableView(tableView
//    override func tableView(tableView: UITableView, commitEditingStyle editingStyle: UITableViewCellEditingStyle, forRowAtIndexPath indexPath: NSIndexPath) {
//        if editingStyle == .Delete {
//            listArray.removeObjectAtIndex(indexPath.row)
//            tableView.deleteRowsAtIndexPaths([indexPath], withRowAnimation: .Fade)
//        } else if editingStyle == .Insert {
//            // Create a new instance of the appropriate class, insert it into the array, and add a new row to the table view.
//        }
//    }


}
//15) Add extenson to hide menu after tap
extension UISplitViewController {
    func toggleMasterView() {
        let barButtonItem = self.displayModeButtonItem()
        UIApplication.sharedApplication().sendAction(barButtonItem.action, to: barButtonItem.target, from: nil, forEvent: nil)
    }
}

