#segment

'''swift
//
//  Homework3ViewController.swift
//  SYStudy
//
//  Created by geonhui Yu on 2022/08/13.
//

import UIKit

class Homework3ViewController: UIViewController {
    
    @IBOutlet weak var resultLabel: UILabel!
    @IBOutlet weak var loader: UIActivityIndicatorView!
    @IBOutlet weak var directionSegment: UISegmentedControl!
    
    private enum Texts {
        
        enum Direction {
            static var east: String {
                return "동쪽"
            }
            static var west: String {
                return "서쪽"
            }
            static var south: String {
                return "남쪽"
            }
            static var north: String {
                return "북쪽"
            }
        }
        
        enum Alert {
            static var title: String {
                return "저장 하시겠습니까?"
            }
            static var message: String {
                return "저장된 정보는 앱이 삭제되기 전까지 지워지지 않습니다."
            }
            static var cancel: String {
                return "취소"
            }
            static var save: String {
                return "저장"
            }
        }
        
        enum Keys {
            static var directionKey: String {
                return "directionKey"
            }
            static var directionIndex: String{
                return "directonIndex"
            }
        }
        
    }
    
    struct Direction {
        let east: String = Texts.Direction.east
        let west: String = Texts.Direction.west
        let south: String = Texts.Direction.south
        let north: String = Texts.Direction.north
    }
//    private var directionKey = "directionKey"
//    private var directionIndex = "directonIndex"
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        loader.hidesWhenStopped = true
        
        resultLabel.text = UserDefaults.standard.string(forKey: Texts.Keys.directionKey) ?? Texts.Direction.east
        directionSegment.selectedSegmentIndex = UserDefaults.standard.integer(forKey: Texts.Keys.directionIndex)
        
        print(UserDefaults.standard.dictionaryRepresentation())
        
//        loader.startAnimating()
//        print(loader.isAnimating)
//        loader.color = .red
    }

    @IBAction func selectDirection(_ sender: UISegmentedControl) {
//        print(sender.selectedSegmentIndex)
//        print(sender.titleForSegment(at: 0))
        
//        guard let value = sender.titleForSegment(at: sender.selectedSegmentIndex) else { return }
//        print(value)
        
        let direction: Direction = Direction()
        
        switch sender.selectedSegmentIndex {
        case 0:
            resultLabel.text = direction.east
        case 1:
            resultLabel.text = direction.west
        case 2:
            resultLabel.text = direction.south
        case 3:
            resultLabel.text = direction.north
        default: break
        }
        
        
    }
    @IBAction func startAnimate(_ sender: Any) {}
    
    @IBAction func stopAnimate(_ sender: Any) {}
    
    @IBAction func saveButton(_ sender: Any) {
        let alert = UIAlertController(title: Texts.Alert.title, message: Texts.Alert.message, preferredStyle: .alert)
        
        let cancel = UIAlertAction(title: Texts.Alert.cancel, style: .cancel)
        let save = UIAlertAction(title: Texts.Alert.save, style: .default) { _ in
            self.showAlert()
        }
        
        alert.addAction(cancel)
        alert.addAction(save)
        present(alert, animated: true)
    }
    
    private func startAnimating() {
        if !loader.isAnimating {
            loader.startAnimating()
            self.view.alpha = 0.7
        }
    }
    
    private func stopAnimating() {
        if loader.isAnimating {
            loader.stopAnimating()
            self.view.alpha = 1.0
        }
    }
    
    private func showAlert() {
        
        startAnimating()
        
        guard let text = resultLabel.text, text.count > 0 else { return }
        UserDefaults.standard.set(text, forKey: Texts.Keys.directionKey)
        
        let idx = directionSegment.selectedSegmentIndex
        UserDefaults.standard.set(idx, forKey: Texts.Keys.directionIndex)
        
        debugPrint("text : \(text), idx: \(idx)")
        DispatchQueue.main.asyncAfter(deadline: DispatchTime.now() + 1) {
            self.stopAnimating()
        }
    }
}

'''
