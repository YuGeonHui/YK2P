#alert

```swift
//
//  Homework2ViewController.swift
//  SYStudy
//
//  Created by geonhui Yu on 2022/08/13.
//

import UIKit

class Homework2ViewController: UIViewController {

    @IBOutlet weak var onOffSwitch: UISwitch!
    
    @IBOutlet weak var onOffButton: UIButton!
    private var state: Bool = false
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
    }
    
    private enum Texts{
        enum alert {
            static var card: String = "설치된 SIM 카드 없음"
        }
        enum alertNum {
            static var number: String = "숫자 선택"
            static var choice: String = "숫자를 선택해주세요"
        }
        enum answer {
            static var check: String = "확인"
            static var cancel: String = "취소"
        }
    }
    
    @IBAction func showAlert(_ sender: Any) {
        
        guard !state else { return }
        
        let alert = UIAlertController(title: Texts.alert.card, message: "", preferredStyle: .alert)
        
        let confirm = UIAlertAction(title: Texts.answer.check, style: .default) { _ in
            self.view.backgroundColor = .yellow
            
            print("qweqweq")
        }
        let cancel = UIAlertAction(title: Texts.answer.cancel, style: .cancel) { _ in
            self.view.backgroundColor = .red
        }
        alert.addAction(confirm)
        alert.addAction(cancel)
        
        present(alert, animated: true, completion: nil)
    }
    
    
    @IBAction func showActionSheet(_ sender: Any) {
        let alert = UIAlertController(title: Texts.alertNum.number, message: Texts.alertNum.choice, preferredStyle: .actionSheet)
        
        let array = ["1", "2", "3", "4"]
        var action = UIAlertAction()
        
        for idx in 0..<array.count {
            action = UIAlertAction(title: array[idx], style: .default)
            alert.addAction(action)
        }
        
        let cancel = UIAlertAction(title: Texts.answer.cancel, style: .cancel)
        alert.addAction(cancel)
        
        present(alert, animated: true)
    }
    
    @IBAction func stateChange(_ sender: Any) {
        state.toggle()
    }
}

```
