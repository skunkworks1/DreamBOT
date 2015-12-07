//
//  ViewController.swift
//  ViewMaster
//
//  Created by Dell Mobility Team - 1 on 11/23/15.
//  Copyright © 2015 Dell. All rights reserved.
//

import UIKit
import AVFoundation
import SpriteKit

class ViewController: UIViewController {
    
    @IBOutlet weak var previousImageView: UIImageView!
    @IBOutlet weak var nextImageView: UIImageView!
    @IBOutlet weak var slideButtonView: UIView!
    @IBOutlet weak var slideButton: UIButton!
    @IBOutlet weak var slidingTextLabel: UILabel!
    @IBOutlet weak var SlidingImage: UIImageView!
    @IBOutlet weak var slidingView: UIView!
    @IBOutlet weak var boarderView: UIView!
    @IBOutlet weak var touchBtn: UIButton!
    
    @IBOutlet weak var backBtn: UIButton!
    @IBOutlet weak var forwardBtn: UIButton!
    
    var bgMusic:AVAudioPlayer = AVAudioPlayer()
    
    var animator:UIDynamicAnimator? = nil;
    var gravity = UIGravityBehavior()
    var collider = UICollisionBehavior()
    let bounce = UIDynamicItemBehavior()
    var snap: UISnapBehavior!
    var barrier: UIView!
    var location = CGPoint(x: 0, y: 0)
    
    var anchorView: UIView!
    var attachment: UIAttachmentBehavior!
    var photocounter=0;
    
    var imageArray: [UIImage] = [
        UIImage(named: "canyon.jpg")!,
        UIImage(named: "Chicago.jpg")!,
        UIImage(named: "Cleveland.jpg")!,
        UIImage(named: "goldengate.jpg")!,
        UIImage(named: "us.jpg")!,
        UIImage(named: "lvegas.jpg")!,
        UIImage(named: "hawai.jpg")!,
        UIImage(named: "rushmore.jpg")!
    ]
    
    var imageNames: [String] = [ "Grand Canyon : The road to the Grand Canyon from the south crosses a gently rising plateau that gives no hint at what is about to unfold.", "Chicago: Chicago, on Lake Michigan in Illinois, is among the largest cities in the U.S.","Cleveland: Cleveland is a city in the U.S. state of Ohio and the county seat of Cuyahoga County, the most populous county in the state.","GoldenGate: The Golden Gate Bridge is a suspension bridge spanning the Golden Gate strait, the one-mile-wide, three-mile-long channel between San Francisco Bay and the Pacific Ocean. ","Statue of Liberty: The Statue of Liberty is a colossal neoclassical sculpture on Liberty Island in New York Harbor in New York City, in the United States." , "Las Vegas: Las Vegas, in Nevada’s Mojave Desert, is a resort town famed for its buzzing energy, 24-hour casinos and endless entertainment options. " , "Hawaii: Hawaii, a U.S. state, is an isolated volcanic archipelago in the Central Pacific. Its islands are renowned for their rugged landscapes of cliffs, waterfalls, tropical foliage and beaches with gold, red, black and even green sands. " , "Mount Rushmore: Mount Rushmore National Memorial is a sculpture carved into the granite face of Mount Rushmore near Keystone, South Dakota, in the United States."]
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        barrier = UIView(frame: CGRect(x: 585, y: 552, width: 100, height: 3))
        barrier.backgroundColor = UIColor.blackColor()
        boarderView.addSubview(barrier)
        
        let line = UIView(frame: CGRect(x: 632, y: 68, width: 3, height: 487))
        line.backgroundColor = UIColor.blackColor()
        boarderView.addSubview(line)
        //slidingView.addSubview(line)
        
        anchorView = UIView(frame: CGRect(x: 300, y: 300, width: 20, height: 20))
        anchorView.backgroundColor = UIColor.whiteColor()
        view.addSubview(anchorView)
        self.anchorView.hidden = true
        
        self.boarderView.layer.borderWidth = 4
        self.boarderView.layer.borderColor = UIColor.blackColor().CGColor
        boarderView.layer.cornerRadius = 10
        boarderView.layer.masksToBounds = true
        
        //Tilt Image if needed
//        previousImageView.transform = CGAffineTransformMakeRotation(0.08);
//        nextImageView.transform = CGAffineTransformMakeRotation(0.08);
    }
    
    
    @IBAction func handlePan(sender: UIPanGestureRecognizer) {
        
        attachment.anchorPoint = sender.locationInView(view)
        anchorView.center = sender.locationInView(view)
        
    }
    
    override func touchesBegan(touches: Set<UITouch>, withEvent event: UIEvent?) {
        
        let touch = touches.first
        location = touch!.locationInView(self.view)
        touchBtn.center = location
        
    }
    
    override func touchesMoved(touches: Set<UITouch>, withEvent event: UIEvent?) {
        
        let touch: UITouch = touches.first! as UITouch
        location = touch.locationInView(self.view)
        touchBtn.center = location

        
    }
    
    func createAnimatorStuff() {
        
        animator = UIDynamicAnimator(referenceView: view)
        gravity = UIGravityBehavior(items: [slideButton])
        animator!.addBehavior(gravity)
        
        collider = UICollisionBehavior(items:[slideButton])
        //collider.collisionDelegate = self
        // add a boundary that has the same frame as the barrier
        collider.addBoundaryWithIdentifier("barrier", forPath: UIBezierPath(rect: barrier.frame))
        collider.translatesReferenceBoundsIntoBoundary = true
        animator!.addBehavior(collider)
        
        let itemBehaviour = UIDynamicItemBehavior(items: [slideButton])
        itemBehaviour.elasticity = 0.3
        animator!.addBehavior(itemBehaviour)
        
        //Animation for bounce back
        UIView.animateWithDuration(0.7, animations:{
            self.slideButton.frame = CGRectMake(self.slideButton.frame.origin.x , self.slideButton.frame.origin.y-500 , self.slideButton.frame.size.width, self.slideButton.frame.size.height)
            
            self.gravity.addItem(self.slideButton);
            self.gravity.gravityDirection = CGVectorMake(0, -0.0)
            self.animator?.addBehavior(self.gravity);
            
        })
        
        //Anchor with gravity behaviour
        
        //        attachment = UIAttachmentBehavior(item: slideButton, attachedToAnchor: CGPointMake(anchorView.center.x,anchorView.center.y))
        //
        //        animator = UIDynamicAnimator(referenceView: view)
        //        animator!.addBehavior(attachment)
        //
        //        gravity = UIGravityBehavior(items: [slideButton])
        //        animator!.addBehavior(gravity)
        
        
    }
    
    func collisionBehavior(behavior: UICollisionBehavior!, beganContactForItem item: UIDynamicItem!, withBoundaryIdentifier identifier: NSCopying?!, atPoint p: CGPoint) {
        print("Boundary contact occurred - \(identifier)")
        
        let collidingView = item as! UIView
        collidingView.backgroundColor = UIColor.yellowColor()
        UIView.animateWithDuration(0.3) {
            collidingView.backgroundColor = UIColor.grayColor()
        }
    }
    
    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
    
    @IBAction func slideTextButtonTapped(sender: UIButton) {
        
        self.slidingTextLabel.slideInFromLeft()
        self.SlidingImage.slideInFromLeft(1.0, completionDelegate: self)
        self.previousImageView.slideInFromLeft(1.0, completionDelegate: self)
        self.nextImageView.slideInFromLeft(1.0, completionDelegate: self)
        
        self.previousImageView.hidden = false
        self.nextImageView.hidden = false
        
        self.slidingTextLabel.text = (imageNames[photocounter])
        SlidingImage.image = (imageArray[photocounter])
        if photocounter != 0
        {
            previousImageView.image = (imageArray[photocounter - 1])
            previousImageView.alpha = 0.5
        } else
        {
            previousImageView.image = UIImage(named: "top10mainpage.jpg")!
            previousImageView.alpha = 0.5
            
            // self.previousImageView.hidden = true
        }
        
        if photocounter != (imageArray.count - 1){
            nextImageView.image = (imageArray[photocounter + 1])
            nextImageView.alpha = 0.5
        }
        else
        {
            nextImageView.image = UIImage(named: "top10mainpage.jpg")!
            nextImageView.alpha = 0.5
            //self.nextImageView.hidden = true
            
        }
        
        photocounter = (photocounter+1)
        createAnimatorStuff()
        if photocounter > imageArray.count - 1
        {
            photocounter=0;
            
        }
        
        print("photocount value is \(photocounter)")
        
        //Add Shutter Sound
        
        let bgMusicURL:NSURL = NSBundle.mainBundle().URLForResource("Shutter", withExtension: "mp3")!
        do { bgMusic = try AVAudioPlayer(contentsOfURL: bgMusicURL, fileTypeHint: nil) } catch _ { return print("file not found") }
        bgMusic.numberOfLoops = 1
        bgMusic.prepareToPlay()
        bgMusic.play()
        
    }
    
    @IBAction func backBtnAction(sender: UIButton) {
        
        self.slidingTextLabel.text = (imageNames[photocounter])
        SlidingImage.image = (imageArray[photocounter])
        self.previousImageView.hidden = true
        self.nextImageView.hidden = true
        
        slidingView = UIImageView(frame: CGRectMake(100, 150, 750, 450))
        
        
        if photocounter > 0 {
            
            photocounter = (photocounter-1)
            
            if photocounter > imageArray.count - 1
            {
                photocounter = 0;
                
            }
        }
        else
        {
            photocounter = 0
            let backAlert = UIAlertController(title: "Alert", message: "This is the first Page. Please view next page.", preferredStyle: UIAlertControllerStyle.Alert)
            
            backAlert.addAction(UIAlertAction(title: "Ok", style: .Default, handler: { (action: UIAlertAction!) in
                print("Handle Ok logic here")
            }))
            
            backAlert.addAction(UIAlertAction(title: "Cancel", style: .Default, handler: { (action: UIAlertAction!) in
                print("Handle Cancel Logic here")
            }))
            
            presentViewController(backAlert, animated: true, completion: nil)
        }
        print("photocount value is \(photocounter)")
        
    }
    
    @IBAction func ForwardBtnAction(sender: UIButton) {
        
        self.slidingTextLabel.text = (imageNames[photocounter])
        SlidingImage.image = (imageArray[photocounter])
        self.previousImageView.hidden = true
        self.nextImageView.hidden = true
        
        slidingView = UIImageView(frame: CGRectMake(100, 150, 650, 450))
        
        photocounter = (photocounter+1)
        
        if photocounter > imageArray.count - 1
        {
            photocounter = (imageArray.count) - 1;
            let frontAlert = UIAlertController(title: "Alert", message: "This is the Last Page. Please view previous page.", preferredStyle: UIAlertControllerStyle.Alert)
            
            frontAlert.addAction(UIAlertAction(title: "Ok", style: .Default, handler: { (action: UIAlertAction!) in
                print("Handle Ok logic here")
            }))
            
            frontAlert.addAction(UIAlertAction(title: "Cancel", style: .Default, handler: { (action: UIAlertAction!) in
                print("Handle Cancel Logic here")
            }))
            
            presentViewController(frontAlert, animated: true, completion: nil)
            
            
        }
        
        print("photocount value is \(photocounter)")
    }
    
    // This function is only called if you set a completionDelegate in your slideInFromLeft() call
    override func animationDidStop(anim: CAAnimation, finished flag: Bool) {
        print("Animation stopped")
    }
    
}

